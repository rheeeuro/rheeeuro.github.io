---
layout: default
title: Canvas Fireworks
nav_order: 8
parent: Canvas
grand_parent: Interactive
---

## Canvas Fireworks

[[출처] How to Code: Realistic Canvas Fireworks](https://youtu.be/R_CnWF3a_ks)

![result](./img/08/01.gif)

### 적용 원리 설명

- x, y, radius, color, velocity, opacity값을 갖는 Particle 오브젝트를 만든다.

- x, y좌표에 radius 크기의 color 색의 opacity 값을 갖는 원을 그리는 draw 메서드를 만든다.

- update 메서드를 만든다. velocity에 friction을 곱한 뒤 velocity.y에는 gravity 값을 더한다. x, y 좌표에 velocity 값을 더하고 opacity 값을 미세하게 낮춘다.

- mouse click 이벤트 리스너를 만든다. 500개의 particle을 만드는데 360도에 500을 나눈 뒤 500개 반복문을 돌면서 마우스 위치에 랜덤 색상을 갖는 x 속도 `Math.cos(radians * i) * (Math.random() * power)` y 속도 `Math.sin(radians * i) * (Math.random() * power)`의 Particle을 만들어준다.

- animate 함수에서 잔상 효과를 위해 clearRect 대신 0.05의 opacity를 갖는 fillRect를 그려주고 Particle들을 update 시켜준다. opacity가 0인 경우 제거해준다.
