---
title: "머신러닝 (Machine Learning)"
categories: 
  - AI
last_modified_at: 2019-10-22T13:00:00+09:00
tags:
- Machine Learning
- AI
toc: true
sidebar_main: true
---

## Intro

> - 머신러닝 이란?



## 머신러닝(Machine Learning)

머신 러닝이란 학습할 데이터를 제공하고 이를 바탕으로 스스로 학습하는 기계를 의미한다.

## 머신러닝 알고리즘

머신러닝의 학습 알고리즘은 `Supervised learning`과 `Unsupervised learning`, `Reinforcement Learning`으로 분류될 수 있다.

> 지도 학습(Supervised Learning)


`Supervised Learning`은 데이터에 대한 `Label(명시적 정답)`이 달려있는 `training set`를 바탕으로 학습시키는 방법이다. 

예를들면 공부시간과 시험점수를 바탕으로 결과를 예측하거나 숫자 이미지를 학습해 맞는 숫자를 예측하는지를 확인할 수 있다.

이 때 시험점수를 예측한다면 `regression(회귀)` 시험을 통과했는지 분류하려면 `binary classification`으로 구분할 수 있다. 또한 등급으로 나눈다면 `multi-label classification`으로 구분된다.


> 비지도 학습(Unsupervised Learning)

`Unsupervised Learning`은 데이터에대한 `Label`이 주어지지 않은 상태에서 학습하는 방법이다. 

예를들면 무작위로 분포된 데이터를 비슷한 특성을 가진 부류로 묶는 `Clustering` 알고리즘이 있다.

이러한 비지도 학습은 데이터에 숨겨진 특징이나 구조를 발견할때 사용된다.

> 강화 학습(Reinforcement Learning)

강화학습은 위의 알고리즘과 다르게 어떤 `에이전트`가 주어진 `환경(Environment)`에서 `행동(Action)`을 취했을 때 `상태(State)`가 변경되고 어떤 `보상(reward)`를 얻으면서 학습한다. 이때 에이전트가 취할수있는 보상을 최대화 하도록 학습이 진행된다. 

## 참고자료

[https://www.techjini.com/blog/machine-learning/](https://www.techjini.com/blog/machine-learning/)

[https://www.youtube.com/watch?v=BS6O0zOGX4E&list=PLlMkM4tgfjnLSOjrEJN31gZATbcj_MpUm&index=1](https://www.youtube.com/watch?v=BS6O0zOGX4E&list=PLlMkM4tgfjnLSOjrEJN31gZATbcj_MpUm&index=1)