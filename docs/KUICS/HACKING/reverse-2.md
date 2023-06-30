---
layout: default
title: '리버스 엔지니어링 2'
nav_order: 3
parent: '기초해킹'
grand_parent: KUICS
---

# 리버스 엔지니어링 2

## CPU에서 우리가 알아야할 두 부분
- 연산 부분 = 계산기
- data 보관 부분 = Register
  - CPU말고도 컴퓨터에는 메모리가 존재함
  - 실행에 필요한 값들이 저장돼있음
    - 코드, 전역변수, 지역변수, ...
  - 레지스터는 메모리와 상호작용함

## CPU 아키텍처 
- CPU 설계방식
- 서로다른 아키텍쳐는 서로 다른 기계어를 사용함
  - Apple M2 -> ARM 아키텍처
  - Intel / AMD Ryzen -> Intel 64bit 아키텍처
  - ARM 아키텍처에서 만든 프로그램을 Intel 64bit 아키텍처에서 실행할 수 없음
    - __기계어가 다르기 때문__
- CPU의 설계목적과 사용환경에 따라 아키텍처가 다르기 때문에 그 종류가 다양한 것
### 32bit vs 64bit 아키텍처
- bit -> CPU가 처리할 수 있는 값이 크기
  - = 레지스터의 크기
  - 32bit 아키텍처는 주소표현을 4GB 까지 밖에 못함
- 우리가 스터디에서 다룰 아키텍처 = Intel 64bit 아키텍처
  - X86_64, AMD64, ...
  - 부르는 이름이 다양
  - 32bit 아키텍처의 하위호환을 지원해줌

## Intel 64bit 아키텍처
### 레지스터
- 레지스터는 일반적으로 범용 레지스터, 세그먼트 레지스터, 인스트럭션 포인터 레지스터가 존재하는데, 여기서는 편하게 두가지로 레지스터를 분류한다.
  - __아무 값이나 담을 수 있는 레지스터__
    - RAX, RBX, RCX, RDX, RDI, RSI, R8, ... , R15
      - R은 64bit를 의미함
  - __특수 값을 담을 수 있는 레지스터__
    - RSP, RBP, RIP
      - P는 Pointer을 의미함
      - 각각 Stack, Base, Instruction
    - RSP와 RBP의 예시
      - <img width="340" alt="image" src="https://github.com/JIEEEN/JIEEEN.github.io/assets/63636210/4cbba824-c794-44a9-8c95-b0a557e612c0">
      - 스택공간에는 함수 호출, 반환에 필요한 정보, 지역변수들이 저장됨
        - 추가로 힙공간에는 동적 할당된 값들, 혹은 아무 값들이나 저장돼있음
      - 스택은 높은주소값에서 낮은주소값으로 자라고, Stack Pointer의 값은 따라서 작아지게 된다.
        - Stack Pointer은 스택의 바닥을 가리킴
      - Base Pointer은 함수의 실행이 종료돼 Caller로 돌아가야하는 곳의 위치를 저장해두어, SP의 위치를 돌려주는 역할을 함
    - RIP의 예시
      - <img width="275" alt="image" src="https://github.com/JIEEEN/JIEEEN.github.io/assets/63636210/1b2fda07-bfd1-4406-893d-ea3be01d843d">
      - 현재 실행하고 있는 Instruction의 주소를 저장
  - 추가로 __RFLAGS__ 라는 레지스터가 존재
    - Zero Flag, Carry Flag, ... 등등을 저장하고 있는 레지스터
- RAX의 하위 4bytes를 EAX와 맞춰줌으로써 하위호환을 지원해줌

## 메모리 구조를 알아야하는 이유
- CPU의 레지스터는 무한하지 않기 때문에, 메모리에서 값을 가져와 레지스터에 저장해 연산을 한다음에 다시 저장하고, 다시 값을 가져오고, ... 의 과정을 반복해야할 수밖에 없음
  - 그렇기 때문에 메모리에 대한 기초적인 이해가 필요하다.

## 섹션
- 프로그램은 메모리에 그대로 올라간다고 생각하면 되는데, 프로그램은 여러 __섹션__ 으로 나누어져 있음
  - 섹션 = 용도가 비슷한 데이터 모임

1. .text 섹션
   - 프로그램 코드에 해당하는 기계어
2. .data 섹션
   - 전역변수 섹션
3. .rdata 섹션
   - 상수 섹션 ("Hello", "1", ...)
   - rdata의 r은 read only

## 어셈블리어
- 명령어와 피연산자로 이루어져있음
  - opcode + operand
  - ex. mov rax, rbx
    - mov = opcode
    - rax, rbx = operand
- __대입 명령어__
  - 레지스터에 있는 값 -> 레지스터
  - 메모리주소에 있는 값 -> 레지스터
  - 레지스터에 있는 값 -> 메모리주소
  - mov(move), lea(load effective address) 
    - mov rax, rbx면 rbx의 값을 rax에 그대로 넣어주면 됨
    - mov rax, [rbx]면 이는 포인터의 값으로 rbx에 저장돼있는 값을 주소로 생각하여, 그 주소에 담겨있는 값을 rax에 복사함
      - [] <- 포인터로 생각하면 됨
    - lea는 기본적으로 mov와 같지만 [] <- 포인터 표시를 무시함
    - lea rax, [rbx] == mov rax, rbx
- __연산 명령어__
  - add, sub, mul, div, ...
  - 비트연산도 존재
    - and, or, xor, not, ...
- __비교 명령어__
  - cmp, test
    - test -> __bitwise and__ 연산
    - cmp -> __뺄셈__ 연산
      - 두 레지스터에 저장돼있는 값이 같은지를 비교하려면, 뺄셈을 하는 것이 가장 간단
      - 연산 결과가 레지스터에 저장되는것이 아닌, RFLAGS 레지스터에 반영됨
  - RFLAGS 레지스터에서 ZFLAG같은 값들은 어디서 사용하나?
    - 분기 구문에서 유용하게 사용할 수 있음
      - 분기를 위해 cmp를 통해 비교해서 ZFLAG가 1이 되면 true block으로, 0이 되면 false block으로 이동하는 방식
- __분기 명령어__
  - jump, jz, jnz, jg, ja, ...
  - 비교 명령어와 섞어서 잘 사용하면 if-else문, for문 등을 어셈블리어로 구현할 수가 있다.