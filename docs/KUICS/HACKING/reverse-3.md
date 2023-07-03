---
layout: default
title: '리버스 엔지니어링 3'
nav_order: 4
parent: '기초해킹'
grand_parent: KUICS
---

# 리버스 엔지니어링 3

## 이번 강의에서 다룰 부분
- 스택조작
- 호출
- 위 두가지에 관한 어셈블리 명령어

## 스택조작
- 스택 = 메모리에 존재하는 스택 공간
  - 스택은 메모리에서 가장 높은 주소에 위치
- 함수의 호출, 반환 정보와 지역변수가 스택공간에 존재한다
- __RSP, RBP__ -> 이 두 레지스터가 스택과 관련됨

### 스택조작 명령어
- push, pop 두가지가 스택조작과 관련된 어셈블리 명령어
- ex)
  - __push 5__, 혹은 __push RAX__
    - 0x1008에 SP가 위치해있을때 push 5 명령어가 처리되면, RSP가 0x1000으로 낮아지면서 0x1000~0x1008에 5라는 값이 위치하게 된다. 
      - 학교 수업시간에 배운 32bit 아키텍처와는 주소 표기 방식이 조금 다른거같다. 32bit에서 주소를 표기할때 0xff라고 하면 이 값은 1바이트를 나타낸다.
    - pop은 이와 반대의 과정

## 함수 호출
- call (주소)
  - ex)
    - 0x1100: __call 0x2000__
      - 0x2000에 F라는 함수가 위치해있다할 때, 0x1100을 Execute하게 되면 0x2000으로 명령어가 Jump하게 돼, code의 flow가 변경된다.
      - 이후 F의 실행이 끝난 후 Return으로 돌아올 때, 0x1108이라는 call의 다음 명령어 주소로 return하게 된다.
      - <img width="208" alt="image" src="https://github.com/JIEEEN/JIEEEN.github.io/assets/63636210/f9aca217-091b-4a3c-a423-32e2b9059590">
      - 이후 위 그림같이 스택공간에 값들이 형성되는데, 보면 F의 스택공간에 F 실행 이후 return할 주소인 0x1108이 포함되는데, 이는 call의 작용이다.
- 인자는 어떻게 세팅하는가?
  - 인자 설정법은 아키텍처마다, 컴파일러마다 다르다.
  - 자주쓰이는 유명한 아키텍처와 컴파일러에 관해 설명해보자.
  - Intel 64bit 기준 + MSVC / GCC
    - MSVC -> RCX, RDX, R8, R9 순으로 전달
        ``` c
            int add(int n1, int n2, int n3, int n4)
                return n1 + n2 + n3 + n4

            add(1, 2, 3, 4)
        ```
        - 위와 같이 c코드가 있다 할 때 이를 어셈블리어로 번역해보면 아래와 같이 된다.
        ``` c
            mov rcx, 1
            mov rdx, 2
            mov r8, 3
            mov r9, 4
            call add
        ```
    - GCC -> RDI, RSI, RDX, RCS 순으로 전달

## 반환
- 반환 관련된 opcode 2개
- __leave, ret__
  - 1. leave
    - leave == mov rsp, rbp + pop rbp
    - mov rsp, rbp
      - F를 수행하면서 sp의 값이 점점 낮아지는데, F를 다 수행하면 이를 다시 bp의 위치로 이동시킬 필요가 있음
    - pop rbp
      - F의 스택공간에 저장돼있던 Main의 bp의 값을 다시 rbp에 저장시킴. 이로써 bp와 sp모두 복원하게 됨
  - 2. ret
    - ret == pop rip
      - F 스택공간의 최상단에 위치해있던 다음 명령어의 값을 읽어옴 -> 의미상으로 반환
