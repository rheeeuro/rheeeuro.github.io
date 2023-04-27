---
layout: default
title: Link Duplicates
nav_order: 13
parent: Blender
---

## Link Duplicates

이제 집들을 복사해서 마을처럼 추가해 줄 예정이다.
일단 크기를 줄여야 하는데 여러 개체를 동시에 줄일 때 전체의 중심점 기준이 아니라 개별 오브젝트의 중심점 기준으로 축소하고 싶은 경우 Snapping 버튼 왼쪽에 있는 `Transform Pivot Point`를 기본값인 `Median Point`에서 `Individual Origins`로 바꾸면 된다. 이후 `G`를 눌러 미세하게 이동시켜주면 다시 Snapping이 된다.

집을 추가하고 싶은 경우 `Ctrl + D`로 복제할 수 있고 필요에 따라 `Alt + D`로 링크된 복사본으로 복사할 수 있다. 링크된 복사본으로 복사한 경우 하나의 객체만 수정해도 링크된 모든 오브젝트들이 업데이트 되는 것을 볼 수 있다.

새로운 오브젝트를 링크하고 싶은 경우 객체가 선택된 상태로 `Shift + Click`을 통해 링크하고 싶은 오브젝트를 선택하고 `Ctrl + L`을 누른 뒤 `Link Object Data`를 누르면 링크를 추가할 수 있다.

//

링크를 해제하고 싶은 경우 `Object - Relations - Make Single User - Object & Data`를 통해 링크를 해제할 수 있다.

//

이후에 같은 Material을 적용하기 위해 링크된 복사본으로 집들을 추가한 모습이다.

..
