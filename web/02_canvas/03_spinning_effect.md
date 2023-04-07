---
layout: default
title: Spinning Effect
nav_order: 1
parent: Canvas
grand_parent: Web
---

## Spinning Effect

[[출처] HTML5 Canvas Vanilla JavaScript Animation - Interactive Animated Background Tutorial for Beginners](https://youtu.be/suBgH07fjmo)

![result](./img/03/01.gif)

### 적용 원리 설명

- 중심으로부터 거리(moveRadius), 단계(step), 각도 위치(position), 원 크기(size)를 속성으로 갖는 Particle 클래스를 만든다.

- 원을 그리는 메서드 draw를 만든다. 화면 중심으로부터 position의 cos, sin을 더한 위치에 size 크기의 원을 그린다.

- update 메서드를 만든다. update 메서드에서는 position에 step을 더해준다.

- init함수에서 랜덤 moveRadius, step, position, size를 갖는 Particle 500개를 만든다.

- requestAnimationFrame 에 등록된 함수에서 Particle별로 update함수와 draw함수를 실행해준다.
