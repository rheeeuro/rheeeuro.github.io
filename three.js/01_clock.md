---
layout: default
title: Clock
nav_order: 1
parent: Three.js
---

## Clock

출처: [Three.js in practice - 3D clock - tutorial for beginners 2022](https://youtu.be/tVgcI_qbSn8)

일단 three.js의 기본 씬 설정 코드이다. three.js를 화면에 띄우기 위해서는 기본적으로 scene, camera, renderer 세 가지가 필요하다.

```js
let scene = new Scene();
scene.background = new Color("white");

let camera = new PerspectiveCamera(45, innerWidth / innerHeight, 0.1, 1000);
// Perspective Camera의 인자로는 fov, aspect ratio, near, far이 있다.
camera.position.set(0, 0, 10);

let renderer = new WebGLRenderer({ antialias: true });
renderer.setSize(innerWidth, innerHeight);
renderer.toneMapping = ACESFilmicToneMapping;
// toneMapping은 HDR 이미지를 HDR을 지원하지 않는 일반모니터에서 추론할 수 있도록 해준다. (default: NoToneMapping)
renderer.outputEncoding = sRGBEncoding;
// 결과물의 인코딩을 정의한다. (default: LinearEncoding)
document.body.appendChild(renderer.domElement);

(function init() {
  renderer.setAnumationLoop(() => {
    renderer.render(scene, camera);
  });
})();
```

orbit control과 PMREMGenerator을 추가해준다.

```js
let controls = new OrbitControls(camera, renderer.domElement);
controls.target.set(0, 0, 0);

let pmrem = new PMREMGenerator(renderer);
// Prefiltered, Minimapped Radiance Environment Map (PMREM)을 생성해 재질의 roughness에 따라 다양한 수준의 블러를 빠르게 적용할 수 있다.
pmrem.compileEquirectangularShader();
// 큐브 맵 셰이더를 미리 컴파일한다. 텍스쳐의 네트워크 로딩 중 메서드를 호출하여 더 빨리 시작할 수 있다.

// in init function
let envHdrTexture = await new RGBELoader().loadAsync(
  "./../assets/vestibule_4k.hdr"
);
// hdr 파일은 poly haven에서 아무거나 가져왔다.
let envRT = pmrem.fromEquirectangular(envHdrTexture);

// in animationloop function
controls.update();
```

다음으로 링을 생성하는 함수를 만들어준다.

```js
function customRing(envRT, thickness, color) {
  let ring = new Mesh(
    new RingGeometry(2, 2 + thickness, 70),
    // RingGeometry의 인자로는 innerRadius, outerRadius, thetaSegments(roundness)가 있다.
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  ring.position.set(0, 0, 0.25 * 0.5);

  // RingGeometry는 2D이므로 입체감을 위해 바깥쪽과 안쪽에 cylinder를 만들어준다.
  let outerCylinder = new Mesh(
    new CylinderBufferGeometry(2 + thickness, 2 + thickness, 0.25, 70, 1, true),
    // 인자는 radiusTop, radiusBottom, height, radialSegments, heightSegments, openEnded
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  outerCylinder.rotation.x = Math.PI * 0.5;

  let innerCylinder = new Mesh(
    new CylinderBufferGeometry(2, 2, 0.25, 140, 1, true),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  innerCylinder.rotation.x = Math.PI * 0.5;

  // 그룹으로 묶어서 리턴
  let group = new Group();
  group.add(ring, outerCylinder, innerCylinder);

  return group;
}
```

마우스의 움직임을 트래킹하는 이벤트 리스너를 추가해준다.

```js
let mousePos = new Vector2(0, 0);
window.addEventListener("mousemove", (e) => {
  // 화면의 중앙을 0, 0으로 설정
  let x = e.clientX - innerWidth * 0.5;
  let y = e.clientY - innerHeight * 0.5;

  // 배율 조정
  mousePos.x = x * 0.001;
  mousePos.y = y * 0.001;
});
```

init 함수에 링을 추가해준다.

```js
// in init function
let ring1 = customRing(envRT, 0.65, "white");
ring1.scale.set(0.75, 0.75);
scene.add(ring1);

let ring2 = customRing(envRT, 0.35, new Color(0.25, 0.225, 0.215));
ring2.scale.set(1.05, 1.05);
scene.add(ring2);

let ring3 = customRing(envRT, 0.15, new Color(0.7, 0.7, 0.7));
ring3.scale.set(1.3, 1.3);
scene.add(ring3);
```

그리고 animation loop 함수에 마우스 포지션에 따른 이동을 반영해준다.

```js
// in animationLoop function
ring1.rotation.x = ring1.rotation.x * 0.95 + mousePos.y * 1.2 * 0.05;
ring1.rotation.y = ring1.rotation.y * 0.95 + mousePos.x * 1.2 * 0.05;

ring2.rotation.x = ring2.rotation.x * 0.95 + mousePos.y * 0.375 * 0.05;
ring2.rotation.y = ring2.rotation.y * 0.95 + mousePos.x * 0.375 * 0.05;

ring3.rotation.x = ring3.rotation.x * 0.95 - mousePos.y * 0.275 * 0.05;
ring3.rotation.y = ring3.rotation.y * 0.95 - mousePos.x * 0.275 * 0.05;
```

다음으로는 시간 표기를 위한 선을 생성하는 함수를 만들어준다.

```js
function customLine(height, width, depth, envRT, color, envMapIntensity) {
  // 박스 위아래로 cylinder를 넣어 뭉뚝한 선을 만들어준다.
  let box = new Mesh(
    new BoxBufferGeometry(width, height, depth),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  box.position.set(0, 0, 0);

  let topCap = new Mesh(
    new CylinderBufferGeometry(width * 0.5, width * 0.5, depth, 10),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  topCap.rotation.x = Math.PI * 0.5;
  topCap.position.set(0, +height * 0.5, 0);

  let bottomCap = new Mesh(
    new CylinderBufferGeometry(width * 0.5, width * 0.5, depth, 10),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  bottomCap.rotation.x = Math.PI * 0.5;
  bottomCap.position.set(0, -height * 0.5, 0);

  let group = new Group();
  group.add(box, topCap, bottomCap);

  return group;
}
```

생성된 선을 움직이는 함수를 만들어준다. (3개의 matrix를 곱해서 이동시켜주는데 이 부분은 이해가 더 필요하다.)

```js
function rotateLine(
  line,
  angle,
  ringRotation,
  topTranslation,
  depthTranslation
) {
  let tmatrix = new Matrix4().makeTranslation(
    0,
    topTranslation,
    depthTranslation
  );
  let rmatrix = new Matrix4().makeRotationAxis(new Vector3(0, 0, 1), -angle);
  let r1matrix = new Matrix4().makeRotationFromEuler(
    new Euler().copy(ringRotation)
  );

  line.matrix.copy(
    new Matrix4().multiply(r1matrix).multiply(rmatrix).multiply(tmatrix)
  );
  line.matrixAutoUpdate = false;
  line.matrixWorldNeedsUpdate = false;
}
```

시침, 분침, 초침을 추가해준다.

```js
// in init function
let hourLine = customLine(0.4, 0.135, 0.07, envRT, "white", 3);
scene.add(hourLine);
let minuteLine = customLine(
  0.8,
  0.135,
  0.07,
  envRT,
  new Color(0.5, 0.5, 0.5),
  1
);
scene.add(minuteLine);
let secoundLine = customLine(
  1,
  0.075,
  0.07,
  envRT,
  new Color(0.2, 0.2, 0.2),
  1
);
scene.add(secoundLine);

// in animationLoop function
let date = new Date();
let hourAngle = (date.getHours() / 12) * Math.PI * 2;
rotateLine(hourLine, hourAngle, ring1.rotation, 1.0, 0);

let minuteAngle = (date.getMinutes() / 60) * Math.PI * 2;
rotateLine(minuteLine, minuteAngle, ring1.rotation, 0.8, 0.1);

let secondAngle = (date.getSeconds() / 60) * Math.PI * 2;
rotateLine(secoundLine, secondAngle, ring1.rotation, 0.75, -0.1);
```

마지막으로 시계의 시간을 표시해 출 선을 추가해준다.

```js
function clockLines(envRT) {
  let group = new Group();

  for (let i = 0; i < 12; i++) {
    let line = customLine(
      0.1,
      0.075,
      0.025,
      envRT,
      new Color(0.65, 0.65, 0.65),
      1
    );
    group.add(line);
  }

  return group;
}

// in init function
let cLines = clockLines(envRT);
scene.add(cLines);

// in animationLoop function
cLines.children.forEach((c, i) => {
  rotateLine(c, (i / 12) * Math.PI * 2, ring1.rotation, 1.72, 0.2);
});
```

마우스 움직임에 따라 회전하는 시계가 완성되었다.

![result](./img/clock.gif)

최종 코드

```js
let scene = new Scene();
scene.background = new Color("white");

let camera = new PerspectiveCamera(45, innerWidth / innerHeight, 0.1, 1000);
camera.position.set(0, 0, 10);

let renderer = new WebGLRenderer({ antialias: true });
renderer.setSize(innerWidth, innerHeight);
renderer.toneMapping = ACESFilmicToneMapping;
renderer.outputEncoding = sRGBEncoding;
document.body.appendChild(renderer.domElement);

let controls = new OrbitControls(camera, renderer.domElement);
controls.target.set(0, 0, 0);

let pmrem = new PMREMGenerator(renderer);
pmrem.compileEquirectangularShader();

let mousePos = new Vector2(0, 0);
window.addEventListener("mousemove", (e) => {
  let x = e.clientX - innerWidth * 0.5;
  let y = e.clientY - innerHeight * 0.5;

  mousePos.x = x * 0.001;
  mousePos.y = y * 0.001;
});

(async function init() {
  let envHdrTexture = await new RGBELoader().loadAsync(
    "./../assets/vestibule_4k.hdr"
  );
  let envRT = pmrem.fromEquirectangular(envHdrTexture);

  let ring1 = customRing(envRT, 0.65, "white");
  ring1.scale.set(0.75, 0.75);
  scene.add(ring1);

  let ring2 = customRing(envRT, 0.35, new Color(0.25, 0.225, 0.215));
  ring2.scale.set(1.05, 1.05);
  scene.add(ring2);

  let ring3 = customRing(envRT, 0.15, new Color(0.7, 0.7, 0.7));
  ring3.scale.set(1.3, 1.3);
  scene.add(ring3);

  let hourLine = customLine(0.4, 0.135, 0.07, envRT, "white", 3);
  scene.add(hourLine);
  let minuteLine = customLine(
    0.8,
    0.135,
    0.07,
    envRT,
    new Color(0.5, 0.5, 0.5),
    1
  );
  scene.add(minuteLine);
  let secoundLine = customLine(
    1,
    0.075,
    0.07,
    envRT,
    new Color(0.2, 0.2, 0.2),
    1
  );
  scene.add(secoundLine);

  let cLines = clockLines(envRT);
  scene.add(cLines);

  renderer.setAnimationLoop(() => {
    ring1.rotation.x = ring1.rotation.x * 0.95 + mousePos.y * 1.2 * 0.05;
    ring1.rotation.y = ring1.rotation.y * 0.95 + mousePos.x * 1.2 * 0.05;

    ring2.rotation.x = ring2.rotation.x * 0.95 + mousePos.y * 0.375 * 0.05;
    ring2.rotation.y = ring2.rotation.y * 0.95 + mousePos.x * 0.375 * 0.05;

    ring3.rotation.x = ring3.rotation.x * 0.95 - mousePos.y * 0.275 * 0.05;
    ring3.rotation.y = ring3.rotation.y * 0.95 - mousePos.x * 0.275 * 0.05;

    let date = new Date();
    let hourAngle = (date.getHours() / 12) * Math.PI * 2;
    rotateLine(hourLine, hourAngle, ring1.rotation, 1.0, 0);

    let minuteAngle = (date.getMinutes() / 60) * Math.PI * 2;
    rotateLine(minuteLine, minuteAngle, ring1.rotation, 0.8, 0.1);

    let secondAngle = (date.getSeconds() / 60) * Math.PI * 2;
    rotateLine(secoundLine, secondAngle, ring1.rotation, 0.75, -0.1);

    cLines.children.forEach((c, i) => {
      rotateLine(c, (i / 12) * Math.PI * 2, ring1.rotation, 1.72, 0.2);
    });

    controls.update();
    renderer.render(scene, camera);
  });
})();

function rotateLine(
  line,
  angle,
  ringRotation,
  topTranslation,
  depthTranslation
) {
  let tmatrix = new Matrix4().makeTranslation(
    0,
    topTranslation,
    depthTranslation
  );
  let rmatrix = new Matrix4().makeRotationAxis(new Vector3(0, 0, 1), -angle);
  let r1matrix = new Matrix4().makeRotationFromEuler(
    new Euler().copy(ringRotation)
  );

  line.matrix.copy(
    new Matrix4().multiply(r1matrix).multiply(rmatrix).multiply(tmatrix)
  );
  line.matrixAutoUpdate = false;
  line.matrixWorldNeedsUpdate = false;
}

function customRing(envRT, thickness, color) {
  let ring = new Mesh(
    new RingGeometry(2, 2 + thickness, 70),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  ring.position.set(0, 0, 0.25 * 0.5);

  let outerCylinder = new Mesh(
    new CylinderBufferGeometry(2 + thickness, 2 + thickness, 0.25, 70, 1, true),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  outerCylinder.rotation.x = Math.PI * 0.5;

  let innerCylinder = new Mesh(
    new CylinderBufferGeometry(2, 2, 0.25, 140, 1, true),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity: 1,
    })
  );
  innerCylinder.rotation.x = Math.PI * 0.5;

  let group = new Group();
  group.add(ring, outerCylinder, innerCylinder);

  return group;
}

function customLine(height, width, depth, envRT, color, envMapIntensity) {
  let box = new Mesh(
    new BoxBufferGeometry(width, height, depth),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  box.position.set(0, 0, 0);

  let topCap = new Mesh(
    new CylinderBufferGeometry(width * 0.5, width * 0.5, depth, 10),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  topCap.rotation.x = Math.PI * 0.5;
  topCap.position.set(0, +height * 0.5, 0);

  let bottomCap = new Mesh(
    new CylinderBufferGeometry(width * 0.5, width * 0.5, depth, 10),
    new MeshStandardMaterial({
      envMap: envRT.texture,
      roughness: 0,
      metalness: 1,
      side: DoubleSide,
      color,
      envMapIntensity,
    })
  );
  bottomCap.rotation.x = Math.PI * 0.5;
  bottomCap.position.set(0, -height * 0.5, 0);

  let group = new Group();
  group.add(box, topCap, bottomCap);

  return group;
}

function clockLines(envRT) {
  let group = new Group();

  for (let i = 0; i < 12; i++) {
    let line = customLine(
      0.1,
      0.075,
      0.025,
      envRT,
      new Color(0.65, 0.65, 0.65),
      1
    );
    group.add(line);
  }

  return group;
}
```
