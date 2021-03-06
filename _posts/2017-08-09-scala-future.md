---
layout: entry
post-category: scala
title: 스칼라 - 퓨처와 동시성
author: 김성중
author-email: ajax0615@gmail.com
description: 스칼라에서 Future(퓨처)를 사용해 동시성을 지원하는 방법에 대한 설명입니다.
publish: true
---

멀티코어 프로세서가 널리 퍼지면서 **동시성**(concurrency)에 대한 관심도 늘어났다. 자바는 공유 메모리(shared memory)와 락(lock)을 기반으로 하는 동시성을 지원하지만, 제대로 사용하기가 아주 어렵다는 사실이 밝혀졌다. 스칼라의 표준 라이브러리는 *Future(퓨처)* 를 사용해 변경 불가능한 상태를 비동기적으로 변환하는 것에 집중하는 방식으로 그런 어려움을 피할 수 있게 해준다.

자바에도 Future가 있지만 스칼라의 것과는 아주 다르다. 두 퓨처 모두 비동기적인 계산의 결과를 표현하지만, 자바의 퓨처에서는 블로킹(blocking) 방식의 get을 사용해 결과를 얻어와야 한다. 자바에서 get을 호출하기 전에 isDone을 호출해 Future가 완료됐는지를 검사할 수 있고, 그에 따라 블로킹을 방지할 수도 있기는 하지만, 계산 결과를 사용해 다른 계산을 수행하려면 Future가 완료되기를 기다려야만 한다.

반면, 스칼라의 Future에서는 계산 결과의 완료 여부와 관계없이 결과 값의 변환을 지정할 수 있다. 각 변환은 원래의 Future를 지정한 함수에 따라 변환한 결과를 비동기적으로 담은 것을 표현하는 새로운 Future를 만든다. 계산을 수행하는 스레드(thread)는 암시적으로 제공되는 **실행 컨텍스트(execution context)** 를 사용해 결정된다. 이런 방식을 사용하면 불변값에 대한 일련의 변환으로 비동기 계산을 표현할 수 있고, 공유 메모리나 락(lock)에 대해 신경을 쓸 필요가 없다.

---

# 골칫거리
자바 플랫폼에서는 각 객체와 연관된 논리적인 **모니터(monitor)** 를 통해 데이터에 대한 여러 스레드의 접근을 제어한다. 이 모델을 사용하려면 어떤 데이터를 공유할지 결정하고, 이 데이터에 접근하거나 제어하는 코드 주변을 synchronized 문으로 감싸야 한다. 자바 런타임은 락 메커니즘을 사용해 동기화 부분을 같은 락으로 보호해서 한 번에 한 스레드만 들어갈 수 있게 보장한다. 이를 통해 여러 스레드의 공유 데이터 접근을 조절할 수 있다.

호환성을 위해 스칼라도 자바의 동시성 기본 요소들을 지원한다. 스칼라에서도 wait, notify, notifyAll 메소드를 사용할 수 있고, 그들 모두 자바와 같은 의미를 갖는다. 기술적으로는 스칼라에 synchronized 키워드가 있는 것은 아니지만, 다음과 같이 사용할 수 있는 synchronized가 이미 정의되어 있다.

```java
var counter = 0
synchronized {
    // 이 안에는 한 번에 한 스레드만 들어올 수 있음
    counter = counter + 1
}
```

불행히도, 프로그래머들은 공유 데이터와 락 모델을 사용해 튼튼한 다중 스레드 애플리케이션을 신뢰성 있게 구축하기가 아주 어렵다는 사실을 알게 됐다. 특히 애플리케이션의 크기와 복잡성이 커지면 상황은 더 나빠진다. 문제는 프로그램의 각 지점에서 여러분이 접근하거나 변경하는 데이터 중 어떤 것을 다른 스레드가 변경하거나 접근할 수 있는지를 추론해야 하고, 어떤 락을 현재 갖고 있는지를 알고 있어야만 한다는 점에 있다. 각 메소드 호출마다 그 메소드가 어떤 락을 가져오려고 하는지 추론하고, 락을 얻는 과정에서 교착 상태(deadlock)에 빠지지 않을 것임을 확신할 수 있어야 한다. 문제를 더 복잡하게 만드는 건, 프로그램이 실행되는 도중에 새로운 락을 얼마든지 만들 수 있기 때문에 여러 분이 고려해야 하는 락이 컴파일 시점에 고정되어 있지 않다는 점이다.

설상가상으로, 다중 스레드 코드에서는 테스트도 신뢰할 수 없다. 스레드가 비결정적이기 때문에, 어떤 프로그램을 테스트할 때 개발자 컴퓨터에서 천 번 성공했더라도 사용자 컴퓨터에서는 첫 번에 잘못될 수도 있다. 공유 데이터와 락이 있는 경우에는 프로그램의 올바름을 논리적으로 따져서 보장해야만 한다.

더 나아가, 동기화를 더 많이 추가한다고 문제를 해결할 수 있는 것도 아니다. 모든 것을 동기화하는 건, 아무것도 동기화하지 않는 것만큼 해롭다. 문제는 새로운 락 연산이 경합 조건(race condition)을 제거할 수 있다고 해도, 동시에 교착 상태의 가능성을 높인다는 점에 있다. 제대로 락을 사용하는 프로그램은 경합도 교착 상태도 없어야 한다. 따라서 어느 한 쪽 방향을 과도하게 추가하는 것만으로는 동기화 문제를 안전하게 풀 수 없다.

java.util.concurrent 라이브러리는 고수준의 동시성 프로그래밍 추상화를 제공한다. 이 동기화 도구를 사용하면 다중 스레드 프로그래밍을할 때 직접 자바의 저수준 동기화 기본 요소를 사용해 직접 추상화된 동기화 기능을 만드는 것보다 훨씬 오류의 여지가 적다. 하지만 동시성 도구도 역시 공유 데이터와 락 모델을 바탕으로 하기 때문에, 그 모델을 사용할 때 발생하는 근본적인 어려움을 해소해주지는 못한다.

---

# 비동기 실행과 Try
모든 문제를 해결할 수 있는 도깨비 방망이는 아니지만, 스칼라의 Future는 공유 데이터와 락의 필요성을 줄여주고, 때로는 아예 없애줄 수도 있는 동시성 처리 방식을 제공한다. 여러분이 스칼라의 메소드를 호출하면 그것은 \'여러분이 기다리는 동안\' 계산을 수행해 결과를 반환한다. 만약 그 결과가 Future라면 그것은 비동기적으로 진행할 다른 계산을 표현하는 것이며, 보통 그런 계산은 별도의 스레드를 통해 이뤄진다. 그 결과 Future에 대한 많은 연산에는 비동기적으로 실행하기 위한 전략을 제공하는 암시적인 **실행 커텍스트(execution context)** 가 필요하다.

Future의 isCompleted와 value라는 메소드를 사용해 폴링(polling)이 가능하다. 아직 완료되지 않은 퓨처에 대해 isCompleted를 호출하면 false를, value를 호출하면 None을 돌려받을 것이다. 퓨처가 완료되고 나면 isCompleted가 true를 반환하며, value는 Some을 반환한다.

그림에서 볼 수 있듯이 Try는 T 타입의 값이 담겨 있는 성공을 나타내는 Success이거나, 예외(java.lang.Throwable의 인스턴스)가 들어있는 실패를 나타내는 Failure 중 하나다. Try의 목적은 동기적 계산에 있는 try 식이 하는 역할을 비동기 계산을 할 떄 제공하는 것이다. 그것을 사용하면 계산이 결과를 정상적으로 반환하지 않고 예외를 발생시키면서 갑자기(abruptly) 완료되는 경우를 처리할 수 있다.

![try](/images/2017/08/09/try.png "try"){: .center-image }

동기적 계산의 경우 try/catch를 사용하면 메소드가 던지는 예외를 그 메소드를 실행하는 스레드 안에서 잡을 수 있다. 하지만 비동기 계산에서는 계산을 시작한 스레드가 다른 작업을 계속 진행하는 경우가 종종 있다. 그래서 그 비동기적 계산이 나중에 예외로 실패할 때 원래의 스레드가 catch 절에서 예외를 처리할 수 없다. 따라서 비동기적 활동을 Future를 사용해 작업하는 경우에는 Try를 사용해서 해당 활동이 값을 만들어 내는 데 실패해 예외를 발생시키면 갑자기 완료되는 상황을 대비해야 한다.

---

# 결론
동시성 프로그래밍은 강력한 기능을 선사한다. 이를 사용하면 코드를 단순화하면서 다중 프로세서의 이점을 누릴 수 있다. 불행히도, 가장 널리 사용되는 동시성 기본 요소인 스레드, 락, 모니터는 교착 상태와 경합으로 가득 찬 지뢰밭이다. Future는 그런 지뢰밭에서 나올 수 있는 한 가지 방법을 제공해서, 여러분이 교착 상태나 경합의 큰 위험 없이도 동시성 프로그램을 작성할 수 있게 해준다.

# 참조
- [Programming in Scala](http://www.acornpub.co.kr/book/programming-in-scala)
