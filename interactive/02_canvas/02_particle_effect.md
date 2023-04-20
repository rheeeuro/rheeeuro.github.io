---
layout: default
title: Particle Effect
nav_order: 2
parent: Canvas
grand_parent: Interactive
---

## Particle Effect

[[출처] Particles JS Effect with Pure Vanilla JavaScript](https://youtu.be/d620nV6bp0A)

![result](./img/02/01.gif)

### 적용 원리 설명

- (x, y)좌표, (x, y)속도, 크기, 색을 속성으로 가지고있는 Particle 클래스를 만든다.

- mousemove 이벤트리스너를 등록해 마우스 좌표를 업데이트해 변수에 담아둔다.

- (x, y) 좌표에 원을 그리는 draw 메서드를 만든다.

- update 메서드를 만들어준다. 벽에 부딫힐경우 속도를 -속도로 바꾸어주고 마우스좌표에서 일정 거리 미만인경우 particle을 밀어낸다.

- connect 함수를 만들어준다. 2중 반복문으로 두 개의 particle 사이의 거리가 일정 거리보다 작을 경우 두 particle 사이를 선으로 이어준다. 거리가 가까울수록 opacity가 증가하고, 멀 수록 opacity가 감소한다.

- init 함수에서 랜덤 좌표, 랜덤 속도를 같는 Particle들을 만들고 requestAnimationFrame 에 등록된 함수에서 Particle별로 update함수와 draw함수를 실행해준다. 마지막으로 connect 함수를 실행해준다.
