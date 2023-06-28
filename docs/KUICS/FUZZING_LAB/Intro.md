---
layout: default
title: Intro
nav_order: 1
parent: FUZZING_LAB
grand_parent: KUICS
---

# Intro

## Fuzzing Lab

<img width="682" alt="image" src="https://github.com/JIEEEN/JIEEEN.github.io/assets/63636210/1febfdb2-3a7c-489d-8ee8-2696f5a7ffad">

- KUICS(고려대), SSG(세종대), SWING(서울여대)이 연합하여 진행하는 2023 하계 여름방학 스터디 중 KUICS에서 담당하는 스터디

## 퍼징이란
- 아직 배우지 않은 단계에서 제대로 설명하지는 못하니 간단하게 얘기해보자면, 수많은 데이터를 프로그램에 주입해 취약점이 밝혀지기를 기도하는 방식이다.
- Black-box, White-box, Grey-box Fuzzing이 있으며, 각각 프로그램에 대해서 아예 모르거나, 전체를 알거나, 내부의 일부를 아는 것이다.
- 정적분석은 오탐(False Positive)의 가능성이 존재하지만, 퍼징의 경우, 그럴 가능성이 현저히 낮다(?).

## 논문 읽는 방법
- 강의자분께 논문 읽는 방법을 소개받았다. 방식이 정해져있는건 아니지만, 추천해준 방식대로 읽으면 목적성에 맞게, 필요한 논문임을 확인하고 읽을 수 있을 것 같았다. 
- 논문은 총 다섯가지 section으로 분류가 가능한데, 아래와 같다.
  - __Abstract__
    - 논문의 핵심을 요약하여 독자에게 제공
  - __Introduction__
    - 연구의 배경에 대해 더 세부적으로 설명
  - __Background__
    - 논문을 읽기 위해 필요한 배경지식, 혹은 새로 제안하는 Notation같은 것들을 제공
  - __Method__
    - 결론을 이끌어내기 위해 실제로 연구에서 수행한 방법(실험 등..)
  - __Conclusion__
    - 연구의 결과
- 위 다섯가지는 실제 논문에 적혀있는 순서 그대로 적은 것인데, 추천하는 방법은 논문을 순서대로 읽는 것이 아니다.
우선 Abstract를 읽어서 어떤 논문인지, 내가 찾는 주제의 논문인지 파악하고, Introduction을 읽는게 아니라 __Conclusion으로 넘어간다__ 
  - 생각보다 Conclusion 단계에서 미적지근한 마무리로 끝을 내는 논문이 많나보다. 
- 이후에는 Introduction -> Background -> Method 순서로 읽어나가면 되는데, Method 부분이 이 논문의 핵심인만큼 집중해서 읽어야다.