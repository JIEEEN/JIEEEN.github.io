---
layout: default
title: 'The Art, Science, and Engineering of Fuzzing: A Survey'
nav_order: 2
parent: FUZZING_LAB
grand_parent: KUICS
---

# The Art, Science, and Engineering of Fuzzing: A Survey

## 논문

<img width="1450" alt="image" src="https://github.com/JIEEEN/JIEEEN.github.io/assets/63636210/506ab4e6-b959-43a6-be76-d1171af7e388">
[논문 링크](https://softsec.kaist.ac.kr/~sangkilc/papers/manes-tse19.pdf)

## 들어가기 전
- Fuzzing Lab에서 2주차에 진입하기 전, 위에 주어진 논문을 읽고 요약해서 정리하며 궁금한 점을 질문하는 과제가 주어졌다. 그리 긴 논문은 아니라고 하지만, 논문을 많이 읽어본 사람들이 아니라는 것을 감안하여 각 파트마다 한명씩, 요약해서 노션에 정리하도록 하게 하였고, 그 중 __PRE_PROCESS__ 부분을 맡게 되었다.
- 이 블로그에서는 위에서 제공된 과제와 상관없이 이전 글에서 작성한대로 Abstract -> Conclusion -> Introduction ... 순서로 읽도록 하겠다.

## Abstract
- _fuzzing_ 은 간단한 개념과 낮은 진입장벽으로 소프트웨어 테스팅 기술 분야에서 현재까지도 매우 유명한 것이다.
- 프로그램을 반복적으로 실행하며 잘못된 input을 넣어주며 테스팅하는 방법
- 퍼징에 관한 관심이 높아져 작업물 또한 방대하게 쏟아짐 -> 너무 복잡하므로 관련된 것들을 일관성 있게 정리하기 위해 분류법을 제시하겠다.
  
## Concluding Remarks
- 이 논문의 목표는 복잡하고 흩어져있는 현대 퍼징에 관한 literature의 일관된 전망을 제시하는 것
- 이를 위해 일반적인 모델을 제시했음
- 이 논문 이후로 퍼징 알고리즘 혹은 용어에 관해 일관성 있게 사용되는 것에 도움이 되기를 바람

## Introduction
- Adobe, Cisco, Google, Microsoft, ... 과 같은 유명한 기업들도 보안과 관련해 퍼징을 사용하는 중임
- 
