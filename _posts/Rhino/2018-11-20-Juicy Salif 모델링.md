---
title: "Rhino Juicy Salif 모델링"
categories: 
  - Rhino
last_modified_at: 2018-11-20T13:00:00+09:00
tags: 
  - Rhino
toc: true
sidebar_main: true
---

## Intro

Juicy Salif 모델링 과정

![juicy](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/230227876.jpg?raw=true)

**Juicy Salif**


## 몸통 스케치

1. 

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/1.png?raw=true)

Front View에서 모델 사진을 가져온 뒤 중심선을 그었다



2.

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/2.png?raw=true)

보간점 커브를 이용해 틀을 그리고 윗부분이 뾰족해지지않게

제어점을 선에대해 수직으로 맞추었다.



3.

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/3.png?raw=true)

구석평면에 수직인 원을 사분점으로부터 만들어 주었다.


4.

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/44.png?raw=true)

Top뷰로와서 원안에 원을 그려주었다.



5.

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/555.png?raw=true)

원형 배열을 통해 360도로 12개의 원을 채웠다.



6.

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/66.png?raw=true)

안쪽 부분을 ``Trim``으로 제거해준다음 (커브도 Trim 할 수 있으니 주의)

바깥 원을 삭제한 뒤 만들어진 모양을 합병해주었다. 



## 몸통 폴리서피스 생성

![7](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/7.png?raw=true)

서피스 도구에서 레일 회전을 선택하고

커브와 원형 틀을 선택 한뒤 서피스를 생성 해주었다.



## 다리 스케치

1.

![8](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/8.png?raw=true)

마찬가지로 보간점 커브를 이용해 다리틀을 그리고


그리고 두 커브사이 중간단계 도구를 이용해 중간 선을 만들어주었다.



2.

![9](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/99.png?raw=true)

끝부분에 구성평면에 수직인 원을 그려주었다. 


3.

![10](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/10.png?raw=true)

Top View로 와서 중심 선을 선택해

원 아래쪽에 붙이고 ``Rotate``를 통해 약간 회전시킨 뒤

``Mirror`` 해주었다.


## 다리 폴리서피스 생성

![11](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/11.png?raw=true)

만들어진 커브 4개를 이용해

``Loft`` 해주었다. (닫힌 로프트 , 타이트하게)

![12](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/12.png?raw=true)
만들어진 서피스를 원형 배열로 360도 3개배치하면 완성


## 완성 예시

![13](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/13.png?raw=true)


**Unreal 임포트**

![14](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/rhino/juicy/unrealrhino.png?raw=true)


