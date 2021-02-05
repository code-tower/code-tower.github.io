---
layout: post
title: "탄력적 검색을 사용하여 앱에서 지리 위치 검색을 설정하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1476973422084-e0fa66ff9456?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDF8fG1hcHxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


위치 기반 기능은 요즘 앱에서 매우 흔합니다. 이러한 기능은 복잡해 보일 수 있지만 Elastic 검색을 통해 쉽게 구현할 수 있습니다.

Elastic search는 문서 기반 구조를 가진 NoSQL 데이터베이스이다. 검색 엔진으로 자주 사용됩니다. 또한 자체 구문과 다양한 도구를 제공하여 검색을 최대한 유연하게 수행할 수 있도록 지원합니다.

이 기사에서는 좌표 범위별 도시 목록을 구해서 지리적 위치별로 검색할 수 있는 간단한 방법을 보여드리겠습니다.

## 탄력적 검색 설치 방법

![image](https://www.freecodecamp.org/news/content/images/2021/01/1-4thJErMA9UpuP1jEBLRWFQ.png)

Elastic search의 웹 사이트에서 쉽게 확인할 수 있는 설치 가이드를 찾을 수 있습니다. 이 기사를 쓸 때 Elastic search 버전 7.4.2를 사용하고 있습니다.

Elastic search는 최근 버전에서 많은 변화를 가져왔으며, 그 중 하나가 매핑 유형 제거라는 점에 유의하십시오. 따라서 Elastic 검색의 다른 버전을 사용하는 경우 여기에 있는 일부 항목이 제대로 작동하지 않을 수 있습니다.

설치를 마친 후에는 설치 안내서에 명확하게 강조되어 있는 Elastic 검색 서비스를 실행하는 것을 잊지 마십시오(Linux의 경우 이 `/bin/elastic search`를 수행합니다.

로컬 컴퓨터의 포트 9200에 대한 GET 요청을 사용하여 탄력적 검색이 실행되고 있는지 확인하십시오. `GET http://localhost:9200`과 같은 경우

## 탄력적 검색 색인 작성 방법

색인은 일반 데이터베이스의 테이블과 유사합니다. 이 예에서는 데이터를 포함할 `city`라는 인덱스를 만들어 보겠습니다.

데이터에 대한 간단한 모델도 정의해 보겠습니다.

- id : 식별자를 위한 id
- `name`: 도시 이름에 대한 텍스트
- `좌표` : 도시 좌표를 저장하는 `좌표_지점` (좌표, 이미 이 데이터 타입을 가지고 있다.

Elastic search에서는 API로 컬을 만들어 인덱스를 만듭니다. 당사의 요청 사항은 다음과 같습니다.

```undefined
PUT http://localhost:9200/cities
```

```undefined
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 1
    },
    "mappings": {
        "properties": {
            "id": {
                "type": "keyword"
            },
            "name": {
                "type": "text"
            },
            "coordinate": {
                "type": "geo_point"
            }
        }
    }
}
```

이 컬을 사용할 때 다음과 같은 응답을 받아 인덱스가 생성되었는지 확인해야 합니다.

```undefined
{
    "acknowledged": true,
    "shards_acknowledged": true,
    "index": "cities"
}

```

잘했어요! 이제 인덱스를 사용할 준비가 되었습니다. 새로 만든 인덱스를 가지고 놀아요.

## 탄력적 검색 데이터를 채우는 방법

이제 Elastic 검색 색인을 문서로 채우겠습니다. 이 용어를 잘 모를 경우 SQL 데이터베이스의 행과 매우 유사하다는 것만 알아두십시오.

Elastic 검색에서는 미리 정의된 스키마와 일치하지 않는 데이터를 저장할 수 있습니다. 그러나 여기서는 이러한 작업을 수행하지 않습니다. 대신 미리 정의된 스키마에 맞는 데이터를 삽입할 것입니다.

한 번에 여러 개의 데이터를 삽입하게 되므로, 한 개의 API 호출에 여러 개의 삽입이 가능한 Elastic search가 제공하는 Bulk API를 사용할 것입니다.

아래 예에서, 저는 9개의 도시를 제 인덱스에 삽입할 것입니다. 원한다면 얼마든지 더 추가하세요.

`POST `http://localhost:9200/city/_bulk`

```undefined
{ "index":{"_index": "cities" } }
{ "id": 1, "name": "Jakarta", "coordinate": {  "lat": -6.2008, "lon": 106.8456}
{ "index":{"_index": "cities" } }
{ "id": 2, "name": "Tokyo", "coordinate": {  "lat": 35.6762, "lon": 139.6503} }
{ "index":{"_index": "cities" } }
{ "id": 3, "name": "Hong Kong", "coordinate": {  "lat": 22.3193, "lon": 114.1694} }
{ "index":{"_index": "cities" } }
{ "id": 4, "name": "New York", "coordinate": {  "lat": 40.7128, "lon": -74.0060} }
{ "index":{"_index": "cities" } }
{ "id": 5, "name": "Paris", "coordinate": {  "lat": 48.8566, "lon": 2.3522} }
{ "index":{"_index": "cities" } }
{ "id": 6, "name": "Bali", "coordinate": {  "lat": -8.3405, "lon": 115.0920} }
{ "index":{"_index": "cities" } }
{ "id": 7, "name": "Berlin", "coordinate": {  "lat": 52.5200, "lon": 13.4050} }
{ "index":{"_index": "cities" } }
{ "id": 8, "name": "San Fransisco", "coordinate": {  "lat": 37.7749, "lon": -122.4194} }
{ "index":{"_index": "cities" } }
{ "id": 9, "name": "Beijing", "coordinate": {  "lat": 39.9042, "lon": 166.4074} }

```

JSON 형식이 잘못되었기 때문에 페이로드가 이상하게 보일 수 있지만 걱정하지 마십시오. 이러한 방식으로 설계되었을 것입니다.

그런 다음 이와 유사한 응답을 보내 회신해야 합니다.

```undefined
{
    "took": 72,
    "errors": false,
    "items": [
        //will contains item for each data inserted
        ...
    ]
}
```

## 탄력적 검색 문서를 쿼리하는 방법

![image](https://images.unsplash.com/photo-1488628176578-4ffd5fdbc900?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDd8fG1hcCUyMHNlYXJjaHxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000)

이제 흥미로운 부분이 나옵니다. 우리는 이전에 삽입한 문서로 질의할 예정입니다.

탄력적 검색은 질의 검색을 위해 다양한 유형의 구문을 지원합니다. 그것은 또한 우리가 오늘 가지고 놀 지리 위치 검색 기능도 가지고 있습니다.

다음과 같은 컬로 간단히 도시 검색을 시작할 수 있습니다.

`POST `http://localhost:9200/city/_search`

```undefined
{
  "query": {
    "bool": {
      "filter": {
        "geo_distance": {
          "distance": "10km",
          "coordinate": {
            "lat": 37.76,
            "lon": -122.42
          }
        }
      }
    }
  }
}
```

그 질문은 저에게 샌프란시스코를 알려주고 좌표는 37.7749와 -122.4194는 저희 좌표에서 반경 10km 이내에 있어야 합니다(구글의 정중함).

```undefined
{
    "took": 7,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 0.0,
        "hits": [
            {
                "_index": "cities",
                "_type": "_doc",
                "_id": "eKPspHYBivyIhfWHb2vl",
                "_score": 0.0,
                "_source": {
                    "id": 8,
                    "name": "San Fransisco",
                    "coordinate": {
                        "lat": 37.7749,
                        "lon": -122.4194
                    }
                }
            }
        ]
    }
}
```

축하합니다! 이제 위치 검색 엔진을 갖게 되었습니다.
하지만 조금 더 실험해 봅시다. 그 장소에 더 많은 도시를 갖고 싶다고 가정해 보자.

페이로드를 변경하여 거리를 4500km까지 확장해 보겠습니다.

```undefined
{
  "query": {
    "bool": {
      "filter": {
        "geo_distance": {
          "distance": "4500km",
          "coordinate": {
            "lat": 37.76,
            "lon": -122.42
          }
        }
      }
    }
  }
}
```

그리고 다음과 같은 응답을 받아야 합니다.

```undefined
{
    "took": 8,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": 0.0,
        "hits": [
            {
                "_index": "cities",
                "_type": "_doc",
                "_id": "dKPspHYBivyIhfWHb2vl",
                "_score": 0.0,
                "_source": {
                    "id": 4,
                    "name": "New York",
                    "coordinate": {
                        "lat": 40.7128,
                        "lon": -74.0060
                    }
                }
            },
            {
                "_index": "cities",
                "_type": "_doc",
                "_id": "eKPspHYBivyIhfWHb2vl",
                "_score": 0.0,
                "_source": {
                    "id": 8,
                    "name": "San Fransisco",
                    "coordinate": {
                        "lat": 37.7749,
                        "lon": -122.4194
                    }
                }
            }
        ]
    }
}
```

두 가지 결과를 제공합니다. 뉴욕과 샌프란시스코. 결과는 정확해 보이지만 위치가 좀 이상할 수 있습니다. 더 가까우니까 샌프란시스코가 우선이겠죠?

글쎄요, 정확히는 아닙니다. 우리가 하고 있는 것은 단지 여과일 뿐이기 때문입니다. 우리의 쿼리는 필터링일 뿐이며 어떤 쿼리가 당신과 가장 가까운지 상관하지 않습니다.

하지만 어떤 위치가 가장 가까운지 계산해 보고 싶다면요? 걱정하지 마세요. Elastic search도 그렇게 할 수 있어요. 함수 점수 쿼리라는 쿼리 유형을 사용할 수 있습니다.

### 탄력적 검색에서 함수 점수 쿼리를 사용하는 방법

탄력적 검색은 사용자에게 표시할 문서를 계산(점수)합니다. 기능 점수 쿼리를 사용하여 해당 점수를 수정하여 반환할 문서를 결정할 수 있습니다.

여기서, 우리는 붕괴 질의 기능을 사용할 것이다. 붕괴 함수에는 세 가지 종류가 있다: exp, 선형, 가우스. 그들 각각은 다른 행동을 한다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/decay_2d.png)

여기서 사용할 것은 선형 유형 함수입니다. 또한 좌표와 오프셋 및 스케일을 함께 지정할 것입니다.

`POST `http://localhost:9200/city/_search`

```undefined
{
  "query": {
    "function_score": {
      "functions": [
        {
          "linear": {
            "coordinate": {
              "origin": "37, -122",
              "offset": "100km",
              "scale":"2500km"
            }
          }
        }
      ],
       "min_score":"0.1"
    }
  }
}
```

이제 우리는 가장 높은 점수로 우리의 결과를 주문 받아야 합니다.

```undefined
{
    "took": 32,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "cities",
                "_type": "_doc",
                "_id": "eKPspHYBivyIhfWHb2vl",
                "_score": 1.0,
                "_source": {
                    "id": 8,
                    "name": "San Fransisco",
                    "coordinate": {
                        "lat": 37.7749,
                        "lon": -122.4194
                    }
                }
            },
            {
                "_index": "cities",
                "_type": "_doc",
                "_id": "dKPspHYBivyIhfWHb2vl",
                "_score": 0.19508117,
                "_source": {
                    "id": 4,
                    "name": "New York",
                    "coordinate": {
                        "lat": 40.7128,
                        "lon": -74.0060
                    }
                }
            }
        ]
    }
}
```

그리고 그것으로 끝이야!

## 결론

이 기사에서는 Elastic 검색을 사용하여 위치 기반 검색을 구현하는 방법에 대해 다룹니다. 하지만 이것이 끝이 아닙니다. 여기서 보여드린 것은 단지 여러분이 할 수 있는 일의 표면일 뿐입니다.

나는 당신이 이 기사가 흥미롭고 유용하다는 것을 알았기를 바랍니다. 그렇다면, 그것에 대해 계속 더 많이 배우고 기능 점수를 조합하는 실험을 해보세요. 재미있을 거야, 약속할게.

> 항상 호기심을 가지면 새로운 것을 배울 수 있을 거야.