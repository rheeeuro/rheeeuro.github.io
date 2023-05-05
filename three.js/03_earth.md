---
layout: default
title: Earth and planes
nav_order: 3
parent: Three.js
---

## Earth and planes

출처: [Three.js in practice - Earth and planes - tutorial for beginners 2022](https://youtu.be/wHjmwEcz4cM)

html에 밝은 배경과 어두운 배경을 만들고 어두운 배경은 opacity를 0으로 둔다.

기본 Three.js Scene을 설정하되 Renderer에 `alpha: true`옵션을 추가해 뒷배경이 보이도록 설정해준다.

구를 하나 추가해주고 OrbitsControl을 추가해준다. 다음과 같은 것을 볼 수 있다.

![result](./img/03/01.png)

https://github.com/Domenicobrz/Threejs-in-practice/tree/main/three-in-practice-3/assets 의 에셋들을 다운받은 뒤, 구에 텍스처를 추가한다.

```js
let textures = {
  bump: await new TextureLoader().loadAsync("assets/earthbump.jpg"),
  map: await new TextureLoader().loadAsync("assets/earthmap.jpg"),
  spec: await new TextureLoader().loadAsync("assets/earthspec.jpg"),
};

let sphere = new Mesh(
  new SphereGeometry(10, 70, 70),
  new MeshPhysicalMaterial({
    map: textures.map,
    roughnessMap: textures.spec,
    bumpMap: textures.bump,
    bumpScale: 0.05,
    sheen: 1,
    sheenRoughness: 0.75,
    sheenColor: new Color("#ff8a00").convertSRGBToLinear(),
    clearcoat: 0.5,
  })
);
```

구에 지구 텍스처가 입혀졌다.

![result](./img/03/02.png)

하지만 뒷편으로 돌리면 검은색만 나오기 때문에 environment map을 추가해줘야 한다.

```js
let pmrem = new PMREMGenerator(renderer);
let envmapTexture = await new RGBELoader()
  .setDataType(FloatType)
  .loadAsync("assets/old_room_2k.hdr");
let envMap = pmrem.fromEquirectangular(envmapTexture).texture;

let sphere = new Mesh(
  new SphereGeometry(10, 70, 70),
  new MeshPhysicalMaterial({
    ...,
    envMap,
    envMapIntensity: 0.4,
  })
);
sphere.rotation.y += Math.PI * 1.25;
```

envmap이 추가되어 검은 부분도 자연스러워지는 것을 볼 수 있다.

![result](./img/03/03.png)
