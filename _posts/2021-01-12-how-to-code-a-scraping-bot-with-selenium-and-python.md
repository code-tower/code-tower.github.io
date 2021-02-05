---
layout: post
title: "Selenium 및 Python으로 Scraping Bot 코딩 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1534723328310-e82dad3ee43f?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDExfHxyb2JvdHxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


Selenium은 웹 응용 프로그램에서 자동화된 테스트를 실행할 수 있도록 설계된 도구입니다. 여러 가지 프로그래밍 언어로 사용할 수 있습니다.

비록 그것이 주된 목적은 아니지만, Selenium은 또한 웹 스크래핑에 사용되는데, 이것은 BeautifulSoup과 같은 일반적인 스크래핑 툴이 할 수 없는 자바스크립트 렌더링 컨텐츠에 접근할 수 있기 때문이다.

셀레늄은 버튼을 클릭하거나 필드를 입력하는 등 데이터를 수집하기 전에 페이지와 상호 작용해야 할 때도 유용합니다. 이것은 이 기사에서 다룰 사용 사례입니다.

예를 들어, 하나 이상의 통화에 대한 달러 환율의 과거 데이터를 추출하기 위해 investing.com을 살펴볼 것입니다.

웹을 검색하면 재무 데이터를 수동으로 스크랩하는 대신 훨씬 쉽게 수집할 수 있는 API 및 Python 패키지를 찾을 수 있습니다. 하지만 셀레늄이 일반적인 데이터 추출에 어떤 도움을 줄 수 있는지 알아보는 것이 좋습니다.

## 스크랩할 웹사이트

먼저, 우리는 웹사이트를 이해해야 합니다. 이 사이트에는 유로 대비 달러 환율에 대한 과거 데이터가 포함되어 있습니다.

이 페이지에서는 원하는 날짜 범위를 설정하는 옵션과 데이터가 있는 테이블을 볼 수 있습니다. 그것이 우리가 사용할 것입니다.

달러 대비 다른 통화에 대한 데이터를 보려면 URL의 다른 통화 코드로 "eur"를 바꾸기만 하면 됩니다.

또한 달러 대비 환율만을 원하는 것으로 가정합니다. 그렇지 않은 경우 URL의 "usd"만 바꾸십시오.

## 스크래퍼 코드

우선 수입부터 시작하죠, 별로 필요 없어요. 셀레늄에서 유용한 아이템 몇 가지를 가져오자. 즉 코드에 일시 중지를 삽입하는 `슬립` 기능과 필요할 때 날짜를 조작하는 `팬더`가 그것이다.

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from time import sleep
import pandas as pd
```

다음에는 데이터를 긁어내는 기능을 쓰겠습니다. 이 기능은 다음을 수신합니다.

- 통화 코드 목록
- 시작일
- 종료일자
- 데이터를 .csv 파일로 내보낼지 여부를 알려주는 부울입니다. False를 기본값으로 사용합니다.

또한, 여러 통화에 대한 데이터를 수집할 수 있는 스크래퍼를 구축하는 것이므로, 빈 목록을 초기화하여 각 통화의 데이터를 저장합니다.

```python
def get_currencies(currencies, start, end, export_csv=False):
    frames = []
```

이 기능에는 통화 목록이 있으므로 이 목록을 반복하여 통화별로 데이터 통화를 얻을 수 있다고 생각할 수 있습니다. 그게 바로 계획이에요.

통화 목록에 있는 각 통화에 대해 URL을 생성하고, 드라이버 개체를 인스턴스화하여 페이지를 가져오는 데 사용합니다. 그러면 창이 최대화되지만 `옵션`을 유지할 경우에만 표시됩니다.머리가 없는 `머리 없는 그렇지 않으면, 셀레늄은 당신에게 아무것도 보여주지 않고 모든 일을 할 것입니다.

```python
for currency in currencies:
    my_url = f'https://br.investing.com/currencies/usd-{currency.lower()}-historical-data'
    option = Options()
    option.headless = False
    driver = webdriver.Chrome(options=option)
    driver.get(my_url)
    driver.maximize_window()
```

우리는 이미 이 시점에서 과거 데이터를 보고 있습니다. 그리고 우리는 단지 데이터와 함께 표를 얻을 수 있습니다. 그러나 기본적으로 지난 20일 동안만 데이터를 볼 수 있습니다. 우리는 이 데이터를 언제든지 받고 싶습니다.

이를 위해 몇 가지 흥미로운 셀레늄 기능을 사용하여 웹 사이트와 상호 작용합니다. 이것이 셀레늄이 빛날 때입니다!

여기서는 날짜를 클릭하고 시작 날짜 및 종료 날짜 필드에 원하는 날짜를 입력하고 적용을 누릅니다.

이를 위해 WebDriverWait, 예상 조건, By를 사용하여 상호 작용할 요소를 클릭할 수 있도록 웹 드라이버가 대기하도록 할 것입니다.

이는 다이버가 클릭이 가능해지기 전에 어떤 것과 상호작용하려고 하면 예외가 제기되기 때문에 중요하다.

대기 시간은 20초이지만, 적절한 시간에 맞춰야 합니다. 먼저 Xpath를 기준으로 날짜 버튼을 선택한 다음 클릭해 보겠습니다.

```python
date_button = WebDriverWait(driver, 20).until(
              EC.element_to_be_clickable((By.XPATH,
              "/html/body/div[5]/section/div[8]/div[3]/div/div[2]/span")))

date_button.click()
```

이제 시작 날짜 필드를 채워야 합니다. 먼저 이 옵션을 선택한 다음 `지우기`를 사용하여 기본 날짜를 삭제하고 `send_keys`를 사용하여 원하는 날짜로 채우도록 하겠습니다.

```python
start_bar = WebDriverWait(driver, 20).until(
            EC.element_to_be_clickable((By.XPATH, 
         "/html/body/div[7]/div[1]/input[1]")))

start_bar.clear()
start_bar.send_keys(start) 
```

이제 종료 날짜 필드에 대해 프로세스를 반복합니다.

```python
end_bar = WebDriverWait(driver, 20).until(
          EC.element_to_be_clickable((By.XPATH, 
          "/html/body/div[7]/div[1]/input[2]")))

end_bar.clear()
end_bar.send_keys(end)
```

이렇게 하면 Apply(적용) 버튼을 선택하고 클릭합니다. 그런 다음 절전 모드를 사용하여 코드를 몇 초 동안 일시 중지하고 새 페이지가 완전히 로드되었는지 확인합니다.

```python
apply_button = WebDriverWait(driver, 20).until(
            EC.element_to_be_clickable((By.XPATH,  
               "/html/body/div[7]/div[5]/a")))

apply_button.click()
sleep(5)
```

`선택권이 있다면``거짓말`인 것처럼 이 모든 과정이 마치 누군가가 페이지를 클릭하는 것처럼 눈앞에 펼쳐지는 것을 볼 수 있을 것이다. Selenium이 Apply(적용)를 클릭하면 지정한 기간의 데이터를 표시하기 위해 테이블이 다시 로드되는 것을 볼 수 있습니다.

이제 `pandas.read_html` 함수를 사용하여 페이지의 모든 테이블을 선택합니다. 이 함수는 페이지의 소스 코드를 수신합니다. 마지막으로, 우리는 운전자를 그만둘 수 있습니다.

```python
dataframes = pd.read_html(driver.page_source)
driver.quit()
print(f'{currency} scraped.')
```

## 셀레늄의 예외 처리 방법

데이터 수집 프로세스가 완료되었습니다. 하지만 셀레늄은 때때로 약간 불안정할 수 있고, 우리가 여기서 수행하는 모든 작업 중에 결국 페이지를 로드하지 못할 수도 있다는 점을 고려해야 합니다.

이를 방지하기 위해 전체 코드를 무한 루프 안에 있는 try 절 안에 넣을 것입니다. 셀레늄이 위에서 설명한 대로 데이터를 수집하면 루프가 끊어집니다. 그러나 문제가 발견될 때마다 기대 조항이 활성화된다.

이 시나리오에서 코드는 다음과 같습니다.

- 드라이버를 종료하십시오. 이렇게 하는 것이 항상 중요하므로 수십 개의 메모리를 사용하는 웹 드라이버가 실행되지 않습니다.
- 오류를 나타내는 메시지 인쇄
- 30초 동안 자세요.
- 루프 시작 부분으로 다시 이동

이 과정은 각 통화에 대한 데이터가 적절하게 수집될 때까지 반복됩니다. 이것이 이 모든 것의 코드입니다.

```python
 for currency in currencies:
        while True:
            try:
                # Opening the connection and grabbing the page
                my_url = f'https://br.investing.com/currencies/usd-{currency.lower()}-historical-data'
                option = Options()
                option.headless = False
                driver = webdriver.Chrome(options=option)
                driver.get(my_url)
                driver.maximize_window()
                   
                # Clicking on the date button
                date_button = WebDriverWait(driver, 20).until(
                            EC.element_to_be_clickable((By.XPATH,
                            "/html/body/div[5]/section/div[8]/div[3]/div/div[2]/span")))
                
                date_button.click()
                
                # Sending the start date
                start_bar = WebDriverWait(driver, 20).until(
                            EC.element_to_be_clickable((By.XPATH,
                            "/html/body/div[7]/div[1]/input[1]")))
                            
                start_bar.clear()
                start_bar.send_keys(start)

                # Sending the end date
                end_bar = WebDriverWait(driver, 20).until(
                            EC.element_to_be_clickable((By.XPATH,
                            "/html/body/div[7]/div[1]/input[2]")))
                            
                end_bar.clear()
                end_bar.send_keys(end)
               
                # Clicking on the apply button
                apply_button = WebDriverWait(driver,20).until(
                  EC.element_to_be_clickable((By.XPATH,
                  "/html/body/div[7]/div[5]/a")))
                
                apply_button.click()
                sleep(5)
                
                # Getting the tables on the page and quiting
                dataframes = pd.read_html(driver.page_source)
                driver.quit()
                print(f'{currency} scraped.')
                break
            
            except:
                driver.quit()
                print(f'Failed to scrape {currency}. Trying again in 30 seconds.')
                sleep(30)
                continue

```

하지만 마지막 한 걸음. 기억하시면 지금까지 DataFramework로 저장된 페이지의 모든 테이블이 포함된 목록입니다. 원하는 과거 데이터가 들어 있는 테이블을 하나 선택해야 합니다.

이 데이터 프레임 목록에 있는 각 데이터 프레임에 대해 열의 이름이 예상과 일치하는지 확인합니다. 만약 그렇다면, 그건 우리의 틀이고 우리는 고리를 끊습니다. 이제 이 DataFrame을 처음에 초기화된 목록에 추가할 준비가 되었습니다.

```python
for dataframe in dataframes:
    if dataframe.columns.tolist() == ['Date', 'Price', 'Open', 'High', 'Low', 'Change%']:
        df = dataframe
        break

frames.append(df)
```

예, export_csv 매개 변수가 True로 설정되어 있으면 .csv 파일을 내보내야 합니다. 그러나 그것은 데이터 프레임과 같은 이슈가 되지는 않는다.to_csv` 메서드는 이 작업을 쉽게 수행할 수 있습니다.

데이터 프레임 목록을 반환하는 것으로 이 기능을 마무리할 수 있습니다. 물론 이 마지막 단계는 통화 목록을 순환하는 것이 끝난 후에 이루어집니다.

```python
if export_csv:
        df.to_csv('currency.csv', index=False)
        print(f'{currency}.csv exported.')

# Outside of the loop
return frames
```

바로 그거야! 다음은 마지막 두 단계를 결합한 전체 코드입니다.

```python
  # Selecting the correct table            
        for dataframe in dataframes:
            if dataframe.columns.tolist() == ['Date', 'Price', 'Open', 'High', 'Low', 'Change%']:
                df = dataframe
                break
        frames.append(df)

        # Exporting the .csv file
        if export_csv:
            df.to_csv('currency.csv', index=False)
            print(f'{currency}.csv exported.')
                  
  return frames
```

## 다음 단계 및 마무리

지금까지 이 코드는 달러 대비 통화 목록의 환율에 대한 과거 데이터를 가져오고 DataFrameworks 및 여러 .csv 파일 목록을 반환합니다.

그러나 항상 개선의 여지가 있습니다. 코드 줄이 몇 줄 더 있으면 함수를 반환하고 목록의 모든 통화에 대한 데이터를 포함하는 단일 DataFrame을 내보내기가 어렵지 않습니다.

또 다른 제안은 기존 데이터 프레임을 수신하는 동일한 셀레늄 기능을 사용하여 `업데이트` 함수를 작성하고 과거 데이터를 현재 날짜로 업데이트하는 것이다.

게다가, 화폐를 긁어내는 데 사용되는 것과 정확히 같은 논리는 주식, 지수, 상품, 선물 등을 긁어내는 데 사용될 수 있다. 네가 긁어낼 수 있는 페이지가 너무 많아.

그러나 서버 과부하를 방지하려면 코드에서 일시 중지를 더 많이 삽입해야 합니다. 또한 Inpatica와 같은 프록시 공급자를 활용하여 스크래치할 페이지가 남아 있는 한 코드가 계속 실행되고 사용자와 사용자의 연결이 보호되도록 해야 합니다.

마지막으로 셀레늄은 웹 사이트에 로그인, 양식 작성, 드롭다운 목록의 항목 선택 등과 같은 여러 다른 상황에서 유용할 수 있다. 물론, 이런 문제에 대한 유일한 해결책은 아니지만, 사용 사례에 따라 분명히 유용할 수 있습니다.

이 기사를 재미있게 보셨기를 바라며, 이 기사가 도움이 되었기를 바랍니다. 질문이나 제안이 있으면 언제든지 연락하세요.