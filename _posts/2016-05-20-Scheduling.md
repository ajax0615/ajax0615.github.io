---
layout: entry
title: 프로세스 스케줄링(Process Scheduling)
author: 김성중
author-email: ajax0615@gmail.com
description: 스케줄링이 무엇이고, 프로세스의 상태 전이에 대한 설명입니다.
publish: true
---

스케줄링(Process Scheduling)이 무엇이고, 프로세스의 상태 전이에 대해서 간단히 알아보겠습니다.

## 스케줄링(Scheduling)

컴퓨터 내의 가장 핵심적인 역할을 담당하는 중앙 처리 장치인 CPU는 사람의 기관에 비유하자면 **'뇌'** 라고 말할 수 있습니다. 사람이 두가지의 생각을 동시에 하지 못하듯, CPU도 마찬가지로 동시에 프로세스를 관리하지 못합니다. 그렇지만, 우리가 보고 있는 이 모니터 화면 안에서는 여러개의 프로그램이 함께 동작하여 작업을 할 수 있게끔 보여지는데 이는 우리가 배우게 될 **'스케줄링(Scheduling)'** 이란 동작 기법을 통해 이와 같은 다중 프로그램을 가능하게 하는 것입니다. 스케줄링은 CPU 이용률을 극대화, 즉 시스템의 자원을 효율적으로 사용하기 위해 어느 프로세스가 CPU를 차지할 것인가에 대한 순서 또는 방법을 결정짓는 작업을 말합니다.

프로세스 스케줄링 기법은 다시 어떤 프로세스가 CPU를 점유할 때 CPU를 빼앗을 수 있느냐, 없느냐에 따라 선점 스케줄링과 비선점 스케줄링으로 나뉘게 됩니다. 여기서 **선점 스케줄링** 은 실행 중인 A와 B라는 프로세스가 있다고 가정을 하게 된다면, A라는 프로세스가 CPU를 점유하고 있는데 B라는 프로세스가 A를 CPU에게서 강제로 떨어트리고 B가 점유를 할 수 있는 방법입니다. 그리고 **비선점 스케줄링** 은 A라는 프로세스가 CPU를 점유하고 있다면, B 프로세스가 CPU를 점유하려고 할때 A의 CPU 점유가 끝날때까지 기다려야 하는 방법입니다.


## 프로세스 상태 전이

어느 시점에서 실행되고 있는 프로세스는 단 한개이며, 여러 개의 프로세스를 번갈아 가며 실행한다는 것을 기억해 두셔야 합니다. 프로세스의 상태 전이는 아래와 같이 New(생성), Ready(준비), Running(실행), Blocked(대기), Terminated(종료)로 나뉘게 됩니다.


![state](/images/2016/05/20/state.PNG "state")

* 생성(New) <br>
 제일 첫번째로 New에서 Ready로 전이되는 과정입니다. 프로세스가 생성되고 나서 생성된 프로세스는 준비(Ready) 상태에 머뭅니다. 준비 상태는 CPU를 점유하고 있는 상태가 아니라, CPU를 점유하길 희망하는 상태입니다. 준비 상태에서 실행 상태로 넘어가려면 작업 스케줄러가 선택해 주어야만 합니다.

* 디스패치(Dispatch) <br>
  디스패치란 준비 상태에서 실행 상태로 전이되는 과정을 말하며, 이는 작업 스케줄러가 해당 프로세스를 선택하여 실행되어지는 것으로, 이때 실행된 프로세스가 CPU를 점유하게 됩니다.

* 인터럽트(Interrupt) <br>
  인터럽트 신호를 받게되면, 실행중이던 프로세스는 준비 상태로 전이되고, 우선순위(Priority)가 높은 프로세스를 실행 상태로 전이시킵니다. (프로세스는 각각 우선순위를 부여받고, 우선순위에 따라 프로세스가 준비 상태로 전이되거나, 실행 상태로 전이됩니다.)

* 입출력 혹은 이벤트 대기(I/O or Event wait) <br>
  CPU를 점유하고 있는 프로세스가 입출력 처리를 해야만 하는 상황이라면, 실행되고 있는 프로세스는 실행 상태에서 대기/보류 상태로 바뀝니다. 그리고 대기 상태로 바뀐 프로세스는 입출력 처리가 모두 끝날때까지 대기 상태로 머뭅니다. 그리고 실행 상태이던 프로세스가 대기 상태로 전이됨과 함께, 준비 상태이던 또다른 프로세스가 실행 상태로 전이됩니다. 또한 대기 상태인 프로세스는 우선순위가 부여되지 않으며 스케줄러에 의해 선택될 수 없습니다.

* 입출력 혹은 이벤트 완료(I/O or Event completion) <br>
  입출력 처리가 끝난 프로세스는 대기 상태에서 준비 상태로 전이되어 스케줄러에게 선택될 수 있게 됩니다. 추가로 프로세스를 종료(Terminate)시킬 때에도 Blocked 상태를 거칠 수 있다는 사실을 기억해 둡시다.
