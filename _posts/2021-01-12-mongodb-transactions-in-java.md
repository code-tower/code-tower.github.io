---
layout: post
title: "Java 코드 불일치를 방지하기 위해 MongoDB에서 트랜잭션을 사용하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1558522195-e1201b090344?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDl8fGhhbmRzfGVufDB8fHw&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


최신 MongoDB 버전 4.2는 다중 문서 트랜잭션을 도입했다. 대부분의 NoSQL 데이터베이스(그리고 SQL DB가 자랑했던)에 없는 주요 기능입니다.

하나 이상의 연산으로 구성될 수 있는 트랜잭션은 원자 연산으로 작동합니다. 모든 하위 작업이 성공하면 해당 트랜잭션이 완료된 것으로 간주됩니다. 그렇지 않으면 실패한다.

이것을 원자성이라고 한다. 데이터를 동시에 읽고 쓸 때 데이터를 일관성 있게 유지하기 위해 이해해야 하는 중요한 개념입니다.

## 문서 범위 및 목표

이 문서의 목적은 트랜잭션 없이 데이터 불일치가 발생하는 실제 사례를 제공하는 것입니다. 그런 다음 우리는 MongoDB Transactions를 사용하여 Java에 솔루션을 구축하여 예방할 것입니다.

이렇게 하면 다음과 같은 방법을 배울 수 있습니다.

- 데이터 불일치를 초래할 수 있는 레이스 조건 방지
- Mongo의 내장 Retryable Writes를 사용하여 보다 탄력적인 애플리케이션 구축

또한 코드 가독성을 향상시키기 위해 사용할 수 있는 래퍼 기능인 `static < R with Transaction(최종 기능 < 클라이언트 세션, R ercedFn)`을 추가하였습니다.

## 예: 동일 은행 계좌에 대한 동시 거래 처리 방법

당신과 당신의 배우자가 공동 은행 계좌를 공유한다고 가정하세요. 여러분 각자가 동시에 현금인출기에 가서 돈을 인출하기 시작합니다.

위의 예에서는 작업이 순차적으로 수행되지 않았습니다. 은행의 P2 프로세스는 P1이 업무를 완료하기를 기다리지 않았다. 만약 은행이 가장 최신의 잔고를 읽기 전에 P1이 잔액을 읽고, 새로운 잔액을 계산하고, 업데이트된 잔액을 DB에 다시 쓰기를 기다렸더라면, 10달러를 잃지 않았을 것입니다.

이 문제의 해결책은 거래입니다. Java의 Locks, Semaphores 및 Synchronized 블록과 비슷하다고 생각할 수 있습니다. Java에서는 Lock 홀더만 잠금으로 보호되는 코드를 실행할 수 있습니다.

## 도우미 기능을 설정하는 방법

이제 코딩 파트에 대해 알아보겠습니다. 몽고 클라이언트를 이미 설정했다고 가정하겠습니다. Java Mongo Driver 3.8 이상이 필요합니다.

getNewClientSession은 단순히 트랜잭션에 대한 세션을 반환합니다. 클라이언트 세션은 특정 트랜잭션의 식별자입니다. 이 데이터는 Mongo 작업이 작업을 격리할 수 있도록 다음 Mongo 작업에 모두 전달하는 중요한 데이터입니다.

getTransactionOptions는 트랜잭션에 대한 옵션을 제공합니다. Read Preference.primary()는 데이터를 읽을 때 클러스터에서 최신 정보를 제공합니다. `고민을 써라."MOST"는 DB가 대부분의 서버에 성공적으로 작성된 후 커밋을 인정하는 결과를 낳는다.

모든 곳에 클라이언트 세션과 트랜잭션 옵션을 만드는 대신, 우리는 그것을 하나의 방법으로 하고 원자성을 필요로 하는 기능들을 그냥 넘겨야 한다.

위의 함수는 전달된 함수인 `executeFn` 인수 내에서 원자 연산 또는 트랜잭션으로 연산을 실행합니다. 거래를 이용한 자금 인출 기능을 구현해 봅시다.

Null을 반환한다는 점에 유의하십시오. 새 예외를 만들어 발신자에게 트랜잭션이 실패했음을 알릴 수 있습니다. 이 예에서 null을 반환하면 트랜잭션 오류가 발생합니다.

## Java의 은행 계정 예제

위의 코드 조각에서 계정 클래스는 사용자 계정에 대한 일반 Java 클래스 모델입니다. 계정 서비스는 계정 수집을 위한 데이터베이스 접근자입니다. `drawCach` 방법은 첫 번째 예에서 설명한 단일 프로세스(P1 또는 P2)에 의해 실행되는 일련의 작업을 완료하여 본인 또는 배우자에게 돈을 분배합니다.

이제 이 `withTransaction` 기능을 사용하여 `drawCache`를 호출합니다.

```undefined
... Some REST API 
AccountService accountService = ...; // Dependency injected

@Path('/account/withdraw') // Endpoint to withdraw money
withdrawMoney() {
 ObjectId accountId = ...// some method to get current users account ID
    Account account = withTransaction(new Function<ClientSession, Account>() {
        @Override
        public Workflow apply(ClientSession clientSession) {
         // Everything inside this block run with in the same transaction as long as you pass the argument clientSession to mongo
            accountService.drawCash(clientSession, accountId, 10);
        }
    });

    if(Objects.isNull(account)){
        return "Failed to withdraw money";
    }
    return "New account balance is " + account.balance;
}
```

이제 이 끝점을 동시에 두 번 호출하면 한 사용자가 최종 잔액을 90으로 보고 두 번째 사용자는 80으로 표시합니다.

두 번째 사용자의 트랜잭션이 실패했다고 추측했을 수 있습니다. 네, 그랬습니다. 그러나 MongoDB에는 기본 제공 재시도 메커니즘이 있으며 자동으로 두 번째 작업을 다시 시도하여 성공했습니다.

## 실제 사용 사례

PS2PDF.com 온라인 비디오 변환기에서 트랜잭션을 사용하여 한 스레드가 다른 스레드에 의해 업데이트된 프로세스 상태를 재정의하지 못하도록 합니다.

예를 들어, 각 비디오 변환 프로세스에 대해 DB에 작업이라는 문서를 작성합니다. STARTED, IN_Progress, Completed 등의 값을 취할 수 있는 상태 필드가 있다.

스레드가 DB의 Job.status를 `COMPLETED`로 업데이트한 후에는 느린 스레드가 해당 메시지를 `IN_PRESSURE`로 되돌리지 않도록 합니다. 작업이 완료되면 변경할 수 없습니다.

위에서 언급한 "With Transaction" 방법을 사용하여 "COMPLY" 상태를 재정의하는 작업이 없음을 보증합니다.

## 결론

이제 애플리케이션의 레이스 상황을 피하기 위해 트랜잭션을 사용할 수 있기를 바랍니다. 또한 내장형 `재시도 쓰기`와 `재시도 읽기`를 사용하여 내결함성을 개선합니다.

저는 MongoDB Transactions는 매우 새로운 것이며, 특별한 상황에서 발생하는 몇 가지 불일치를 식별하는 기사들이 있다는 것을 지적해야 합니다. 그러나 이러한 문제에 부딪힐 가능성은 거의 없습니다.