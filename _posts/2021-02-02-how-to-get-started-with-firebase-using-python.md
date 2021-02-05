---
layout: post
title: "Python을 사용하여 Firebase를 시작하는 방법
 "
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1523861751938-121b5323b48b?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDJ8fGZpcmV8ZW58MHx8fA&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


이 문서는 Firebase 데이터베이스를 설정하고 Python을 사용하여 간단한 CRUD 작업을 수행하는 데 도움이되는 자세한 가이드입니다.
 

아시다시피 Firebase는 앱 개발을 가속화하기 위해 Google에서 제공하는 플랫폼입니다.
 BaaS 또는 백엔드를 서비스로 제공하므로 Firebase가 클라우드 인프라와 모든 백엔드 요구 사항을 처리합니다.
 이를 통해 더 빠르게 개발하고 배포 할 수 있습니다.
 

Firebase는 실시간 데이터베이스, Cloud Firestore, 인증과 같은 몇 가지 놀라운 제품을 제공합니다.
 또한 호스팅을 허용하고 텍스트 인식, 이미지 라벨링 등과 같은 기계 학습 작업을위한 API를 제공합니다!
 

여기에 링크 된 사이트로 이동하여 사용 가능한 멋진 옵션을 살펴보십시오.
 

## Firebase 실시간 데이터베이스를 설정하는 방법
 

Firebase에 새 프로젝트를 만듭니다. 이름을 BookStoreProject로 지정하겠습니다.
 설정이 완료되면 데이터베이스 만들기 옵션을 선택하여 실시간 데이터베이스를 만듭니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/pic-1.png)

데이터베이스 생성을 클릭하면 데이터베이스의 위치와 보안 규칙을 지정해야합니다.
 두 가지 규칙을 사용할 수 있습니다.
 

- 잠금 모드는 데이터베이스에 대한 모든 읽기 및 쓰기를 거부합니다.
 
- 테스트 모드는 기본 30 일 동안 읽기 및 쓰기 액세스를 허용합니다 (그 이후에는 보안 규칙이 업데이트되지 않는 한 모든 읽기 및 쓰기가 거부 됨).
 

읽기, 쓰기 및 편집을 위해 데이터베이스를 사용할 것이므로 테스트 모드를 선택합니다.
 이 작업이 완료되면 데이터베이스를 사용할 준비가 된 것입니다!
 

## Python을 사용하여 Firebase 실시간 데이터베이스에 쓰는 방법
 

바로 다음 단계는 Python을 사용하여 데이터베이스에 연결할 수있는 방법을 찾는 것입니다.
 Admin Database API를 사용하겠습니다.
 필요한 라이브러리를 설치해야합니다.
 

Python 용 `firebase_admin`사용에 대한 자세한 내용은 여기에 링크 된 공식 문서를 확인하세요.
 

```python
pip install firebase_admin
```

Firebase에 연결하려면 다음 코드 줄이 필요합니다.
 

```undefined
import firebase_admin

cred_obj = firebase_admin.credentials.Certificate('....path to file')
default_app = firebase_admin.initialize_app(cred_object, {
 'databaseURL':databaseURL
 })
```

그러나 코드가 작동하도록하려면 몇 가지 전제 조건이 필요합니다.
 

먼저 admin SDK를 초기화하는 데 사용할 서비스 계정 키의 경로를 지정해야합니다.
 

Firebase는 Google 서비스 계정에서 Firebase 서버 API에 대한 액세스를 허용합니다.
 서비스 계정을 인증하려면 JSON 형식의 개인 키가 필요합니다.
 

자격 증명 개체를 만들려면이 JSON 파일의 경로를 제공해야합니다.
 키를 생성하려면 프로젝트 설정으로 이동하여 새 개인 키 생성을 클릭하고 파일을 다운로드 한 후 디렉토리 구조에 배치하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-205.png)

이 프로세스에 대한 자세한 설명은 여기에 링크 된 공식 문서를 참조하십시오.
 

다음으로 데이터베이스에 대한 액세스를 제공하는 URL 인 databaseURL이 필요합니다.
 실시간 데이터베이스 Firebase 콘솔 페이지 자체에 있습니다.
 

### set () 함수를 사용하여 작성하는 방법
 

```undefined
from firebase_admin import db

ref = db.reference("/")
```

데이터베이스의 루트에 대한 참조를 설정합니다 (또는 키 값 또는 하위 키 값으로 설정할 수도 있음).
 자연스럽게 발생하는 질문은 실시간 데이터베이스에 데이터를 저장하는 데 어떤 스키마가 허용됩니까?
 

저장할 모든 데이터는 JSON 형식, 즉 키 값 쌍의 시퀀스 여야합니다.
 시스템 생성 키가 필요한 경우 곧 다룰`push ()`함수를 사용하도록 선택할 수 있습니다.
 

데이터베이스에 저장할 수있는 적합한 JSON을 구성 해 보겠습니다.
 4 권의 책에 관한 정보는 다음과 같습니다.
 

```undefined
{
 "Book1":
 {
  "Title": "The Fellowship of the Ring",
  "Author": "J.R.R. Tolkien",
  "Genre": "Epic fantasy",
  "Price": 100
 },
 "Book2":
 {
  "Title": "The Two Towers",
  "Author": "J.R.R. Tolkien",
  "Genre": "Epic fantasy",
  "Price": 100 
 },
 "Book3":
 {
  "Title": "The Return of the King",
  "Author": "J.R.R. Tolkien",
  "Genre": "Epic fantasy",
  "Price": 100
 },
 "Book4":
 {
  "Title": "Brida",
  "Author": "Paulo Coelho",
  "Genre": "Fiction",
  "Price": 100
 }
}
```

필요한 JSON 파일을로드하고 다음과 같이 데이터베이스에 데이터를 저장합니다.
 

```undefined
import json
with open("book_info.json", "r") as f:
 file_contents = json.load(f)
ref.set(file_contents)
```

이제 데이터베이스는 다음과 같습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-207.png)

### push () 함수를 사용하여 작성하는 방법
 

Firebase는 고유 한 시스템 생성 키로 데이터를 저장하는`push ()`함수를 제공합니다.
 이 방법을 사용하면 동일한 키에 대해 여러 쓰기가 수행되는 경우 자신을 덮어 쓰지 않습니다.
 

예를 들어 여러 소스가 / Books / Best_Sellers /에 쓰기를 시도하면 마지막 쓰기를 수행하는 소스가 데이터베이스에 유지됩니다.
 이로 인해 데이터를 덮어 쓸 가능성이 있습니다.
 `push ()`는 추가 된 각각의 새 하위 항목에 대해 고유 한 키를 사용하여이 문제를 해결합니다.
 

```undefined
ref = db.reference("/")
ref.set({
 "Books":
 {
  "Best_Sellers": -1
 }
})

ref = db.reference("/Books/Best_Sellers")
import json
with open("book_info.json", "r") as f:
 file_contents = json.load(f)

for key, value in file_contents.items():
 ref.push().set(value)
```

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-208.png)

`push ()`및`set ()`은 원 자성이 아닙니다.
 즉, 두 기능이 하나의 분할 할 수없는 단위로 중단없이 함께 실행된다는 보장이 없습니다.
 

데이터베이스가 업데이트되는 동안 데이터를 가져 오려고하면`push ()`가 완료되었지만`set ()`은 완료되지 않았을 수 있습니다. 따라서 수신 한 JSON에는 값이없는 시스템 생성 키가 있습니다.
 들.
 

## Python을 사용하여 Firebase 데이터베이스를 업데이트하는 방법
 

데이터베이스 업데이트는 필요한 지점에 참조를 설정하고`update ()`함수를 사용하는 것만 큼 간단합니다.
 J.R.R. Tolkien의 책 가격이 할인을 제공하기 위해 80 단위로 인하되었다고 가정 해 보겠습니다.
 

```undefined
ref = db.reference("/Books/Best_Sellers/")
best_sellers = ref.get()
print(best_sellers)
for key, value in best_sellers.items():
 if(value["Author"] == "J.R.R. Tolkien"):
  value["Price"] = 90
  ref.child(key).update({"Price":80})
        
        
```

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-209.png)

## Python을 사용하여 Firebase에서 데이터를 검색하는 방법
 

특정 키를 업데이트하려고 할 때`get ()`메소드를 사용하여 이미 데이터를 검색했습니다.
 이제 몇 가지 방법을 더 살펴보고 복잡한 쿼리를 만들기 위해 함께 결합합니다.
 

`order_by_child ()`메소드를 사용하여 모든 책을 가격순으로 정렬 해 보겠습니다.
 이 방법을 적용하려면 먼저 Firebase 보안 규칙의`.indexOn` 규칙을 통해 색인 필드로 정렬하는 키를 설정해야합니다.
 

가격별로 정렬하려면 가격이 인덱스로 나열되어야합니다.
 다음과 같이 값을 설정할 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-210.png)

```undefined
ref = db.reference("/Books/Best_Sellers/")
print(ref.order_by_child("Price").get())
```

메서드의 반환 값은 OrderedDict입니다.
 키로 정렬하려면`order_by_key ()`를 사용하십시오.
 최고 가격으로 책을 얻으려면 다음과 같이`limit_to_last ()`메서드를 사용합니다.
 

```undefined
ref.order_by_child("Price").limit_to_last(1).get()
```

또는 가장 저렴한 책을 얻기 위해 다음과 같이 작성합니다.
 

```undefined
ref.order_by_child("Price").limit_to_first(1).get()
```

정확히 80 단위로 책정 된 책을 얻으려면 다음을 사용합니다.
 

```undefined
ref.order_by_child("Price").equal_to(80).get()
```

요구 사항에 따라 데이터베이스를 쿼리하는 더 많은 예제와 방법은 여기에서 공식 문서를 확인하십시오.
 

## Python을 사용하여 Firebase에서 데이터를 삭제하는 방법
 

데이터 삭제는 매우 간단합니다.
 J.R.R.로 베스트셀러 책을 모두 삭제합시다.
 저자로 Tolkien.
 

```undefined
ref = db.reference("/Books/Best_Sellers")

for key, value in best_sellers.items():
 if(value["Author"] == "J.R.R. Tolkien"):
  ref.child(key).set({})
        
        
```

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-211.png)

## 결론
 

이 게시물에서는 Firebase 실시간 데이터베이스를 만들고 데이터로 채우고 Python을 사용하여 데이터를 삭제, 업데이트 및 쿼리하는 방법을 배웠습니다.
 

Firebase의 아름다움을 방금 발견했지만 선택할 수있는 다양한 옵션과 방법에 압도당하는 Python 개발자에게 도움이되기를 바랍니다.
 여기까지 읽으 셨다면 정말 감사합니다!
 조심 하시고 즐거운 코딩을하세요!
 