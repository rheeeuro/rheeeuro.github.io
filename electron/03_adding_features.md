---
layout: default
title: Adding Features
nav_order: 3
parent: Electron
---

## Adding Features

여기서 앱의 기능과 복잡도를 추가하기 위해서는 두 가지 옵션이 있다.

1. 웹 앱 코드의 renderer 프로세스에 로직을 추가
2. 운영체제, Node.js와의 더욱 긴밀한 통합

1번의 경우 Electron 관련 리소스들은 더이상 필요하지 않게 된다. 그냥 Electron은 웹 앱을 실행시켜주는 역할만 하고 나머지는 HTML, CSS, Javascript의 동일한 툴들로 웹 앱을 만들면 된다.

2번의 경우 Electron이 제공하는 툴들을 사용할 수 있다. 아이콘에서부터 단축키, 어플리케이션 메뉴 등을 만들 수 있다. Node.js 환경의 파워를 메인 프로세스에 이용할 수 있다.
