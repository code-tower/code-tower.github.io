---
layout: post
title: "Java의 가비지 콜렉션 – GC 란 무엇이며 JVM에서 작동하는 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/GC.png
tags: undefined
---


이전 기사에서 Java Virtual Machine (JVM)에 대해 작성하고 아키텍처에 대해 설명했습니다.
 Execution Engine 구성 요소의 일부로 Java GC (가비지 수집기)에 대해서도 간략하게 설명했습니다.
 

이 기사에서는 가비지 콜렉터, 작동 방식, Java에서 사용할 수있는 다양한 유형의 GC 및 그 장점에 대해 자세히 알아 봅니다.
 또한 최신 Java 릴리스에서 사용할 수있는 새로운 실험용 가비지 수집기 중 일부를 다룰 것입니다.
 

가비지 컬렉션은 사용하지 않는 개체를 삭제하여 런타임에 사용되지 않은 메모리를 회수하는 프로세스입니다.
 

C 및 C ++와 같은 언어에서 프로그래머는 객체의 생성과 소멸을 모두 담당합니다.
 때로는 프로그래머가 쓸모없는 객체를 파괴하는 것을 잊고 할당 된 메모리가 해제되지 않을 수 있습니다.
 시스템의 사용 된 메모리는 계속 증가하고 결국 할당 할 메모리가 시스템에 남아 있지 않습니다.
 이러한 응용 프로그램은 "메모리 누수"를 겪습니다.
 

일정 시점이 지나면 새로운 객체 생성에 충분한 메모리를 사용할 수 없으며 OutOfMemoryErrors로 인해 전체 프로그램이 비정상적으로 종료됩니다.
 

C에서는`free ()`, C ++에서는`delete ()`와 같은 메서드를 사용하여 가비지 수집을 수행 할 수 있습니다.
 Java에서 가비지 콜렉션은 프로그램 수명 동안 자동으로 발생합니다.
 이렇게하면 메모리 할당을 해제 할 필요가 없으므로 메모리 누수가 방지됩니다.
 

Java Garbage Collection은 Java 프로그램이 자동 메모리 관리를 수행하는 프로세스입니다.
 Java 프로그램은 JVM (Java Virtual Machine)에서 실행할 수있는 바이트 코드로 컴파일됩니다.
 

Java 프로그램이 JVM에서 실행되면 프로그램 전용 메모리의 일부인 힙에 개체가 생성됩니다.
 

Java 애플리케이션의 수명 동안 새 객체가 생성되고 릴리스됩니다.
 결국 일부 개체는 더 이상 필요하지 않습니다.
 어느 시점에서든 힙 메모리는 두 가지 유형의 객체로 구성되어 있다고 말할 수 있습니다.
 

- 라이브-이 객체는 다른 곳에서 사용되고 참조됩니다.
 
- Dead-이 개체는 더 이상 사용되거나 어디에서나 참조되지 않습니다.
 

가비지 수집기는 이러한 사용하지 않는 개체를 찾아 삭제하여 메모리를 확보합니다.
 

가비지 컬렉션의 주요 목적은 참조를 포함하지 않는 개체를 삭제하여 힙 메모리를 해제하는 것입니다.
 개체에 대한 참조가 없으면 죽은 것으로 간주되어 더 이상 필요하지 않습니다.
 따라서 객체가 차지하는 메모리를 회수 할 수 있습니다.
 

객체에 대한 참조를 해제하여 가비지 컬렉션 후보로 만들 수있는 다양한 방법이 있습니다.
 그들 중 일부는 다음과 같습니다.
 

### 참조를 null로 만들어
 

```undefined
Student student = new Student();
student = null;
```

### 다른 사람에게 참조를 할당하여
 

```undefined
Student studentOne = new Student();
Student studentTwo = new Student();
studentOne = studentTwo; // now the first object referred by studentOne is available for garbage collection
```

### 익명 개체를 사용하여
 

```undefined
register(new Student());
```

Java 가비지 콜렉션은 자동 프로세스입니다.
 프로그래머는 삭제할 객체를 명시 적으로 표시 할 필요가 없습니다.
 

가비지 콜렉션 구현은 JVM에 있습니다.
 각 JVM은 자체 버전의 가비지 콜렉션을 구현할 수 있습니다.
 그러나 힙 메모리에있는 개체로 작업하고, 연결할 수없는 개체를 표시하거나 식별하고, 압축을 통해 제거하는 표준 JVM 사양을 충족해야합니다.
 

## Java에서 가비지 콜렉션 루트 란 무엇입니까?
 

가비지 수집기는 GC 루트 (Garbage Collection Roots)의 개념에 대해 작업하여 라이브 개체와 죽은 개체를 식별합니다.
 

이러한 가비지 컬렉션 루트의 예는 다음과 같습니다.
 

- 시스템 클래스 로더에 의해로드 된 클래스 (사용자 정의 클래스 로더가 아님)
 
- 라이브 스레드
 
- 현재 실행중인 메소드의 지역 변수 및 매개 변수
 
- JNI 메소드의 지역 변수 및 매개 변수
 
- 글로벌 JNI 참조
 
- 동기화를위한 모니터로 사용되는 개체
 
- 목적을 위해 JVM이 가비지 콜렉션에서 보유한 오브젝트
 

가비지 수집기는 해당 가비지 컬렉션 루트에서 시작하여 루트에서 다른 개체에 대한 참조를 따라 메모리의 전체 개체 그래프를 탐색합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-76.png)

## Java의 가비지 수집 단계
 

표준 가비지 컬렉션 구현에는 세 단계가 포함됩니다.
 

### 개체를 살아있는 것으로 표시
 

이 단계에서 GC는 개체 그래프를 탐색하여 메모리의 모든 라이브 개체를 식별합니다.
 

GC가 객체를 방문하면 액세스 가능하고 따라서 활성 상태로 표시됩니다.
 가비지 수집기가 방문하는 모든 개체는 살아있는 것으로 표시됩니다.
 GC Roots에서 도달 할 수없는 모든 개체는 가비지이며 가비지 수집 후보로 간주됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-82.png)

### 죽은 물체 청소
 

마킹 단계 후에는 라이브 (방문한) 개체와 죽은 (방문하지 않은) 개체가 차지하는 메모리 공간이 있습니다.
 스윕 단계는 이러한 죽은 개체를 포함하는 메모리 조각을 해제합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-83.png)

### 메모리에 남아있는 개체 압축
 

스윕 단계에서 제거 된 죽은 개체가 반드시 서로 옆에있을 필요는 없습니다.
 따라서 조각난 메모리 공간이 생길 수 있습니다.
 

가비지 수집기가 죽은 개체를 삭제 한 후 메모리를 압축 할 수 있으므로 나머지 개체는 힙 시작시 연속 블록에있게됩니다.
 

압축 프로세스를 사용하면 새 개체에 순차적으로 메모리를 쉽게 할당 할 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-85.png)

Java Garbage Collector는 개체를 연령별로 분류하는 세대 별 가비지 수집 전략을 구현합니다.
 

JVM의 모든 개체를 표시하고 압축하는 것은 비효율적입니다.
 점점 더 많은 개체가 할당됨에 따라 개체 목록이 늘어나 가비지 수집 시간이 길어집니다.
 애플리케이션의 경험적 분석에 따르면 Java의 대부분의 개체는 수명이 짧습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/ObjectLifetime.gif)

위의 예에서 Y 축은 할당 된 바이트 수를 나타내고 X 축은 시간에 따라 할당 된 바이트 수를 나타냅니다.
 보시다시피 시간이 지남에 따라 점점 더 적은 수의 개체가 할당됩니다.
 

실제로 대부분의 개체는 그래프의 왼쪽에있는 더 높은 값에서 알 수 있듯이 수명이 매우 짧습니다.
 이것이 Java가 객체를 세대로 분류하고 그에 따라 가비지 수집을 수행하는 이유입니다.
 

JVM의 힙 메모리 영역은 세 섹션으로 나뉩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-70.png)

## 젊은 세대
 

새로 만들어진 개체는 Young Generation에서 시작됩니다.
 Young Generation은 다음과 같이 세분화됩니다.
 

- Eden 공간-모든 새 개체가 여기에서 시작되고 초기 메모리가 할당됩니다.
 
- 생존자 공간 (FromSpace 및 ToSpace)-하나의 가비지 수집주기에서 살아남은 후 Eden에서 개체가 여기로 이동합니다.
 

개체가 Young Generation에서 가비지 수집되면 사소한 가비지 수집 이벤트입니다.
 

Eden 공간이 객체로 채워지면 Minor GC가 수행됩니다.
 모든 죽은 개체가 삭제되고 모든 라이브 개체가 생존 공간 중 하나로 이동됩니다.
 Minor GC는 또한 생존자 공간에있는 개체를 확인하고 다른 생존자 공간으로 이동합니다.
 

다음 순서를 예로 들어 보겠습니다.
 

- Eden에는 모든 개체가 있습니다 (살아 있거나 죽었 음)
 
- 마이너 GC 발생-모든 죽은 개체가 Eden에서 제거됩니다.
 모든 라이브 개체는 S1 (FromSpace)로 이동됩니다.
 Eden과 S2는 이제 비어 있습니다.
 
- 새 개체가 생성되고 Eden에 추가됩니다.
 Eden 및 S1의 일부 개체가 죽습니다.
 
- Minor GC 발생-모든 죽은 개체가 Eden 및 S1에서 제거됩니다.
 모든 라이브 개체는 S2 (ToSpace)로 이동됩니다.
 Eden과 S1은 이제 비어 있습니다.
 

따라서 언제든지 생존자 공간 중 하나는 항상 비어 있습니다.
 살아남은 물체가 생존자 공간을 돌아 다니는 특정 임계 값에 도달하면 구세대로 이동합니다.
 

`-Xmn` 플래그를 사용하여 Young Generation의 크기를 설정할 수 있습니다.
 

## 구세대
 

수명이 긴 물건은 결국 젊은 세대에서 구세대로 옮겨집니다.
 이것은 Tenured Generation으로도 알려져 있으며 오랫동안 생존자 공간에 남아 있던 물체를 포함합니다.
 

개체가 구세대로 이동하기 전에 얼마나 많은 가비지 수집주기를 유지할 수 있는지를 결정하는 개체의 사용 기간에 대해 정의 된 임계 값이 있습니다.
 

개체가 구세대에서 가비지 수집되는 경우 주요 가비지 수집 이벤트입니다.
 

`-Xms` 및`-Xmx` 플래그를 사용하여 힙 메모리의 초기 및 최대 크기를 설정할 수 있습니다.
 

Java는 세대 별 가비지 수집을 사용하기 때문에 개체가 더 많은 가비지 수집 이벤트를 유지할수록 힙에서 더 많이 승격됩니다.
 그것은 젊은 세대에서 시작하여 충분히 오래 살아남 으면 결국 종신 세대로 끝납니다.
 

공간과 세대 간의 객체 승격을 이해하려면 다음 예를 고려하십시오.
 

객체가 생성되면 먼저 젊은 세대의 에덴 공간에 놓입니다.
 사소한 가비지 수집이 발생하면 Eden의 라이브 개체가 FromSpace로 승격됩니다.
 다음 사소한 가비지 수집이 발생하면 Eden과 FromSpace의 라이브 개체가 ToSpace로 이동됩니다.
 

이주기는 특정 횟수 동안 계속됩니다.
 이 시점 이후에도 개체가 계속 사용되면 다음 가비지 수집주기에서 개체를 이전 생성 공간으로 이동합니다.
 

## 영구 세대
 

클래스 및 메소드와 같은 메타 데이터는 영구 세대에 저장됩니다.
 애플리케이션에서 사용중인 클래스를 기반으로 런타임시 JVM에 의해 채워집니다.
 더 이상 사용되지 않는 클래스는 영구 세대에서 가비지 수집 될 수 있습니다.
 

`-XX : PermGen` 및`-XX : MaxPermGen` 플래그를 사용하여 영구 세대의 초기 및 최대 크기를 설정할 수 있습니다.
 

## MetaSpace
 

Java 8부터 MetaSpace 메모리 공간이 PermGen 공간을 대체합니다.
 구현은 PermGen과 다르며 힙의이 공간은 이제 자동으로 크기가 조정됩니다.
 

이는 힙의 PermGen 공간의 제한된 크기로 인해 메모리가 부족한 애플리케이션 문제를 방지합니다.
 Metaspace 메모리는 가비지 수집 될 수 있으며 더 이상 사용되지 않는 클래스는 Metaspace가 최대 크기에 도달하면 자동으로 정리 될 수 있습니다.
 

가비지 콜렉션은 힙 메모리에서 참조되지 않은 오브젝트를 제거하고 새 오브젝트를위한 여유 공간을 만들기 때문에 Java 메모리를 효율적으로 만듭니다.
 

Java Virtual Machine에는 8 가지 유형의 가비지 수집기가 있습니다.
 각각을 자세히 살펴 보겠습니다.
 

## 직렬 GC
 

이것은 GC의 가장 간단한 구현이며 단일 스레드 환경에서 실행되는 소규모 응용 프로그램을 위해 설계되었습니다.
 모든 가비지 수집 이벤트는 하나의 스레드에서 연속적으로 수행됩니다.
 압축은 각 가비지 수집 후에 실행됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-68.png)

실행되면 전체 응용 프로그램이 일시 중지되는 "세계 중지"이벤트로 이어집니다.
 전체 애플리케이션이 가비지 수집 중에 고정되므로 지연 시간이 짧은 실제 시나리오에서는 권장되지 않습니다.
 

Serial Garbage Collector를 사용하기위한 JVM 인수는`-XX : + UseSerialGC`입니다.
 

## 병렬 GC
 

병렬 수집기는 다중 프로세서 또는 다중 스레드 하드웨어에서 실행되는 중간 크기에서 대규모 데이터 세트가있는 애플리케이션을위한 것입니다.
 이것은 JVM에서 GC의 기본 구현이며 처리량 수집기라고도합니다.
 

Young Generation에서는 소규모 가비지 수집에 여러 스레드가 사용됩니다.
 단일 스레드는 구세대의 주요 가비지 수집에 사용됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-66.png)

Parallel GC를 실행하면 "세계 중지 이벤트"가 발생하고 응용 프로그램이 중지됩니다.
 다중 스레드 환경에 더 적합하므로 일괄 작업 실행과 같이 많은 작업을 수행해야하고 긴 일시 중지가 허용되는 경우에 사용할 수 있습니다.
 

병렬 가비지 콜렉터를 사용하기위한 JVM 인수는`-XX : + UseParallelGC`입니다.
 

## 병렬 구형 GC
 

이것은 Java 7u4 이후 Parallel GC의 기본 버전입니다.
 Young Generation과 Old Generation 모두에 다중 스레드를 사용한다는 점을 제외하면 Parallel GC와 동일합니다.
 

병렬 가비지 수집기를 사용하기위한 JVM 인수는`-XX : + UseParallelOldGC`입니다.
 

## CMS (동시 마크 스윕) GC
 

이를 동시 낮은 일시 중지 수집기라고도합니다.
 병렬과 동일한 알고리즘을 사용하여 사소한 가비지 콜렉션에 다중 스레드가 사용됩니다.
 주요 가비지 수집은 Parallel Old GC와 같이 다중 스레드 방식이지만 CMS는 응용 프로그램 프로세스와 함께 동시에 실행되어 "세계 중지"이벤트를 최소화합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-67.png)

이 때문에 CMS 수집기는 다른 GC보다 더 많은 CPU를 사용합니다.
 더 나은 성능을 위해 더 많은 CPU를 할당 할 수 있다면 CMS 가비지 수집기가 병렬 수집기보다 더 나은 선택입니다.
 CMS GC에서는 압축이 수행되지 않습니다.
 

Concurrent Mark Sweep Garbage Collector를 사용하기위한 JVM 인수는`-XX : + UseConcMarkSweepGC`입니다.
 

## G1 (쓰레기 우선) GC
 

G1GC는 CMS를 대체하기 위해 고안되었으며 사용 가능한 큰 힙 크기 (4GB 이상)가있는 다중 스레드 응용 프로그램을 위해 설계되었습니다.
 CMS와 같이 병렬적이고 동시 적이지만 이전 가비지 수집기와 비교하면 내부에서 상당히 다르게 작동합니다.
 

G1도 세대 적이지만 젊은 세대와 노인 세대를위한 별도의 지역이 없습니다.
 대신 각 세대는 지역의 집합으로, 유연한 방식으로 젊은 세대의 크기를 조정할 수 있습니다.
 

힙을 동일한 크기의 영역 세트 (힙 크기에 따라 1MB에서 32MB까지)로 분할하고 여러 스레드를 사용하여 스캔합니다.
 지역은 프로그램이 실행되는 동안 언제든지 이전 지역 또는 젊은 지역 일 수 있습니다.
 

표시 단계가 완료된 후 G1은 가장 많은 가비지 개체가 포함 된 영역을 알고 있습니다.
 사용자가 최소 일시 중지 시간에 관심이있는 경우 G1은 일부 지역 만 대피하도록 선택할 수 있습니다.
 사용자가 일시 중지 시간에 대해 걱정하지 않거나 상당히 큰 일시 중지 시간 목표를 언급 한 경우 G1은 더 많은 지역을 포함하도록 선택할 수 있습니다.
 

G1GC는 가장 많은 가비지가있는 지역을 식별하고 먼저 해당 지역에서 가비지 수집을 수행하므로 가비지 우선이라고합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-88.png)

Eden, Survivor 및 Old 메모리 영역 외에도 G1GC에는 두 가지 유형의 영역이 더 있습니다.
 

- Humongous-대형 오브젝트 (힙 크기의 50 %보다 큼)에 사용됩니다.
 
- 사용 가능-사용되지 않거나 할당되지 않은 공간
 

G1 가비지 콜렉터를 사용하기위한 JVM 인수는`-XX : + UseG1GC`입니다.
 

## Epsilon 가비지 수집기
 

Epsilon은 JDK 11의 일부로 출시 된 아무것도하지 않는 (no-op) 가비지 수집기입니다. 메모리 할당을 처리하지만 실제 메모리 회수 메커니즘을 구현하지는 않습니다.
 사용 가능한 Java 힙이 모두 소모되면 JVM이 종료됩니다.
 

개발자가 애플리케이션 메모리 풋 프린트를 정확히 알고 있거나 심지어 완전히 가비지없는 애플리케이션을 보유하고있는 극도로 지연 시간에 민감한 애플리케이션에 사용할 수 있습니다.
 다른 시나리오에서는 Epsilon GC를 사용하지 않는 것이 좋습니다.
 

Epsilon Garbage Collector를 사용하기위한 JVM 인수는`-XX : + UnlockExperimentalVMOptions -XX : + UseEpsilonGC`입니다.
 

## 셰넌 도어
 

Shenandoah는 JDK 12의 일부로 출시 된 새로운 GC입니다. G1에 비해 Shenandoah의 주요 이점은 애플리케이션 스레드와 동시에 가비지 수집주기 작업을 더 많이 수행한다는 것입니다.
 G1은 애플리케이션이 일시 중지 된 경우에만 힙 영역을 비울 수있는 반면, Shenandoah는 애플리케이션과 동시에 개체를 재배치 할 수 있습니다.
 

Shenandoah는 사용 가능한 메모리를 감지 한 후 거의 즉시 라이브 개체를 압축하고, 쓰레기를 정리하고, RAM을 OS로 되돌릴 수 있습니다.
 이 모든 것이 응용 프로그램이 실행되는 동안 동시에 발생하기 때문에 Shenandoah는 CPU를 더 많이 사용합니다.
 

Epsilon Garbage Collector를 사용하기위한 JVM 인수는`-XX : + UnlockExperimentalVMOptions -XX : + UseShenandoahGC`입니다.
 

## ZGC
 

ZGC는 JDK 11의 일부로 출시되었으며 JDK 12에서 개선 된 또 다른 GC입니다. 짧은 대기 시간 (10ms 미만 일시 중지) 및 / 또는 매우 큰 힙 (수 테라 바이트)을 사용하는 애플리케이션을위한 것입니다.
 

ZGC의 주요 목표는 짧은 대기 시간, 확장 성 및 사용 용이성입니다.
 이를 위해 ZGC는 Java 애플리케이션이 모든 가비지 수집 작업을 수행하는 동안 계속 실행되도록 허용합니다.
 기본적으로 ZGC는 사용되지 않은 메모리를 해제하고 운영 체제에 반환합니다.
 

따라서 ZGC는 매우 낮은 일시 중지 시간 (일반적으로 2ms 이내)을 제공하여 다른 기존 GC보다 크게 개선되었습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/figure2_600w.jpg)

Epsilon Garbage Collector를 사용하기위한 JVM 인수는`-XX : + UnlockExperimentalVMOptions -XX : + UseZGC`입니다.
 

참고 : Shenandoah와 ZGC는 모두 프로덕션 기능으로 만들어지고 JDK 15의 실험 단계에서 벗어날 예정입니다.
 

애플리케이션에 엄격한 일시 중지 시간 요구 사항이없는 경우 애플리케이션을 실행하고 JVM이 올바른 수집기를 선택하도록 허용해야합니다.
 

대부분의 경우 기본 설정이 정상적으로 작동합니다.
 필요한 경우 힙 크기를 조정하여 성능을 향상시킬 수 있습니다.
 성능이 여전히 목표를 충족하지 못하면 애플리케이션 요구 사항에 따라 수집기를 수정할 수 있습니다.
 

- 직렬-응용 프로그램에 작은 데이터 세트 (최대 약 100MB)가 있거나 일시 중지 시간 요구 사항없이 단일 프로세서에서 실행되는 경우
 
- 병렬-최대 애플리케이션 성능이 우선이고 일시 중지 시간 요구 사항이 없거나 1 초 이상의 일시 중지가 허용되는 경우
 
- CMS / G1-전체 처리량보다 응답 시간이 더 중요하고 가비지 수집 일시 중지를 약 1 초 미만으로 유지해야하는 경우
 
- ZGC-응답 시간이 높은 우선 순위이고 / 또는 매우 큰 힙을 사용하는 경우
 

Java에서 가비지 콜렉션의 여러 이점이 있습니다.
 

우선, 코드를 간단하게 만듭니다.
 적절한 메모리 할당 및 릴리스주기에 대해 걱정할 필요가 없습니다.
 코드에서 객체 사용을 중지하면 사용중인 메모리가 어느 시점에서 자동으로 회수됩니다.
 

가비지 수집이없는 언어 (예 : C 및 C ++)로 작업하는 프로그래머는 코드에서 수동 메모리 관리를 구현해야합니다.
 

또한 가비지 수집기가 힙 메모리에서 참조되지 않은 개체를 제거하기 때문에 Java 메모리를 효율적으로 만듭니다.
 이렇게하면 새 개체를 수용 할 수 있도록 힙 메모리가 해제됩니다.
 

일부 프로그래머는 가비지 수집보다 수동 메모리 관리를 선호한다고 주장하지만 가비지 수집은 이제 많은 인기 프로그래밍 언어의 표준 구성 요소입니다.
 

가비지 수집기가 성능에 부정적인 영향을 미치는 시나리오의 경우 Java는 효율성을 향상시키기 위해 가비지 수집기를 튜닝하는 많은 옵션을 제공합니다.
 

## 수동 트리거 방지
 

가비지 콜렉션의 기본 메커니즘 외에도 Java에서 가비지 콜렉션에 대해 이해해야 할 가장 중요한 점 중 하나는 비 결정적이라는 것입니다.
 즉, 런타임에 가비지 콜렉션이 발생할시기를 예측할 방법이 없습니다.
 

`System.gc ()`또는`Runtime.gc ()`메서드를 사용하여 가비지 수집기를 실행하기위한 힌트를 코드에 포함 할 수 있지만 가비지 수집기가 실제로 실행된다는 보장은 없습니다.
 

## 분석 도구 사용
 

응용 프로그램을 실행할 메모리가 충분하지 않으면 속도 저하, 긴 가비지 수집 시간, "세계 중지"이벤트 및 결국 메모리 부족 오류가 발생합니다.
 이는 힙이 너무 작다는 것을 나타낼 수 있지만 애플리케이션에서 메모리 누수가 있음을 의미 할 수도 있습니다.
 

`jstat` 또는 Java Flight Recorder와 같은 모니터링 도구에서 도움을 받아 힙 사용량이 무한히 증가하는지 확인할 수 있습니다. 이는 코드의 버그를 나타낼 수 있습니다.
 

## 기본 설정이 좋음
 

작은 독립형 Java 응용 프로그램을 실행하는 경우 가비지 수집 조정이 필요하지 않을 것입니다.
 기본 설정은 잘 작동합니다.
 

## 튜닝에 JVM 플래그 사용
 

Java 가비지 콜렉션을 조정하는 가장 좋은 방법은 JVM에서 플래그를 설정하는 것입니다.
 플래그는 사용할 가비지 수집기 (예 : Serial, G1 등), 힙의 초기 및 최대 크기, 힙 섹션의 크기 (예 : Young Generation, Old Generation) 등을 조정할 수 있습니다.
 

## 올바른 수집기 선택
 

조정되는 응용 프로그램의 특성은 설정에 대한 좋은 초기 가이드입니다.
 예를 들어, 병렬 가비지 수집기는 효율적이지만 종종 "세계 중지"이벤트를 유발하므로 가비지 수집을위한 긴 일시 중지가 허용되는 백엔드 처리에 더 적합합니다.
 

반면에 CMS 가비지 수집기는 일시 중지를 최소화하도록 설계되어 응답 성이 중요한 웹 기반 애플리케이션에 이상적입니다.
 

이 기사에서는 Java Garbage Collection, 작동 방식 및 다양한 유형에 대해 설명했습니다.
 

많은 간단한 응용 프로그램에서 Java 가비지 수집은 프로그래머가 의식적으로 고려해야 할 사항이 아닙니다.
 그러나 Java 기술을 향상시키려는 프로그래머의 경우 Java 가비지 수집이 작동하는 방식을 이해하는 것이 중요합니다.
 

이것은 또한 백엔드 역할에 대한 주니어 및 시니어 레벨 모두에서 매우 인기있는 인터뷰 질문입니다.
 

지금까지 함께 해주셔서 감사합니다.
 기사가 마음에 들었기를 바랍니다.
 기술과 생활에 대해 정기적으로 논의하는 LinkedIn에서 나와 연결할 수 있습니다.
 다른 기사와 YouTube 채널도 살펴보세요.
 행복한 독서.
 🙂
 