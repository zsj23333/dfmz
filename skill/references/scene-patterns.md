# Scene Patterns

## Procedural Textures

All textures are generated procedurally using canvas 2D:

### Sky Texture

```javascript
function texSky() {
  const c = cvs(2048, 1024), x = c.getContext('2d');
  const g = x.createLinearGradient(0, 0, 0, c.height);
  g.addColorStop(0, '#0a0e14');
  g.addColorStop(0.5, '#1a2a3a');
  g.addColorStop(1, '#2a3a4a');
  x.fillStyle = g;
  x.fillRect(0, 0, c.width, c.height);
  // Add stars
  for (let i = 0; i < 200; i++) {
    x.fillStyle = `rgba(255,255,255,${Math.random() * 0.8})`;
    x.beginPath();
    x.arc(Math.random() * c.width, Math.random() * c.height * 0.5, Math.random() * 1.5, 0, Math.PI * 2);
    x.fill();
  }
  return new THREE.CanvasTexture(c);
}
```

### Concrete Texture

```javascript
function texConcrete(seed) {
  const rnd = mulberry32(seed);
  const c = cvs(512, 512), x = c.getContext('2d');
  x.fillStyle = '#2a2a2a';
  x.fillRect(0, 0, c.width, c.height);
  // Add noise
  for (let i = 0; i < 10000; i++) {
    const v = rnd() * 30;
    x.fillStyle = `rgba(${v},${v},${v},0.3)`;
    x.fillRect(rnd() * c.width, rnd() * c.height, 1, 1);
  }
  return new THREE.CanvasTexture(c);
}
```

### Glass Texture

```javascript
function texGlass(seed) {
  const rnd = mulberry32(seed);
  const c = cvs(512, 512), x = c.getContext('2d');
  x.fillStyle = '#1a2a3a';
  x.fillRect(0, 0, c.width, c.height);
  // Add windows
  for (let i = 0; i < 50; i++) {
    const w = 20 + rnd() * 40;
    const h = 30 + rnd() * 60;
    const px = rnd() * c.width;
    const py = rnd() * c.height;
    x.fillStyle = `rgba(255,200,100,${0.1 + rnd() * 0.3})`;
    x.fillRect(px, py, w, h);
  }
  return new THREE.CanvasTexture(c);
}
```

## Common Scene Patterns

### Tower Pattern

```javascript
function buildTower(x, z, h) {
  const g = new THREE.Group();
  const mat = surface(libn('glass', () => texGlass(101)), [1, 1.4], {
    color: 0x7fa3b5, roughness: .35, metalness: .55
  });
  const geo = new THREE.BoxGeometry(3, h, 3);
  const mesh = new THREE.Mesh(geo, mat);
  mesh.position.y = h / 2;
  g.add(mesh);
  g.position.set(x, 0, z);
  scene.add(g);
}
```

### Stadium Pattern

```javascript
function buildStadium(x, z) {
  const g = new THREE.Group();
  // Base
  const base = new THREE.Mesh(
    new THREE.CylinderGeometry(22, 24, 3, 64),
    steelMat
  );
  base.position.y = 1.5;
  g.add(base);
  // Seats
  const seats = new THREE.InstancedMesh(
    new THREE.BoxGeometry(0.6, 0.4, 0.6),
    seatMat,
    2000
  );
  g.add(seats);
  g.position.set(x, 0, z);
  scene.add(g);
}
```

### Water Pattern

```javascript
function buildWater(x, z) {
  const mat = surface(libn('water', () => texWater()), [80, 60], {
    color: 0x0c1620, roughness: .42, metalness: .30
  });
  const bed = new THREE.Mesh(new THREE.PlaneGeometry(420, 300), mat);
  bed.rotation.x = -Math.PI / 2;
  bed.position.set(x, -0.06, z);
  scene.add(bed);
}
```

## Camera Paths

### Hero Approach

```javascript
const WPS = [
  { p: [0, 8, 28], f: [0, 14, -40], fov: 34 },  // Start far
  { p: [0, 14, 18], f: [0, 12, -40], fov: 52 },  // Close on subject
  { p: [-18, 10, 12], f: [-18, 16, -44], fov: 42 },  // Fly around
  { p: [0, 22, 8], f: [0, 8, -40], fov: 46 },  // Look down
  { p: [0, 30, 38], f: [0, 10, -40], fov: 44 },  // Pull back
  { p: [0, 36, 52], f: [0, 8, -40], fov: 48 }   // Far view
];
```

### Aerial View

```javascript
const WPS = [
  { p: [0, 50, 0], f: [0, 0, 0], fov: 60 },  // Top-down
  { p: [30, 40, 30], f: [0, 0, 0], fov: 50 },  // Angle
  { p: [0, 30, 50], f: [0, 0, 0], fov: 40 },  // Side
  { p: [-30, 40, 30], f: [0, 0, 0], fov: 50 },  // Other side
  { p: [0, 50, 0], f: [0, 0, 0], fov: 60 }   // Back to top
];
```

## Post-Processing

### Bloom

```javascript
POST.matCompose = mk(
  'uniform sampler2D tDiffuse,tB0,tB1,tB2,tB3; uniform float w0,w1,w2,w3;' +
  'uniform float exposure,bloom,time; varying vec2 vUv;' +
  'void main(){ vec3 c=texture2D(tDiffuse,vUv).rgb;' +
  'vec3 b=texture2D(tB0,vUv).rgb*w0 + texture2D(tB1,vUv).rgb*w1 + texture2D(tB2,vUv).rgb*w2 + texture2D(tB3,vUv).rgb*w3;' +
  'c+=b*bloom; c*=exposure;' +
  'c=c/(c+vec3(.92));' +
  'float l=dot(c,vec3(.2126,.7152,.0722));' +
  'vec3 cool=vec3(.955,1.0,1.06); vec3 warm=vec3(1.06,1.0,.93);' +
  'c=mix(c*cool,c*warm,smoothstep(.05,.72,l));' +
  'c=mix(c,c*vec3(1.0,.985,.94),smoothstep(.62,1.0,l)*.5);' +
  'vec2 q=vUv-.5; float d=dot(q,q); c*=1.0-smoothstep(.26,.9,d*1.4);' +
  'c+=vec3(.007,.009,.016); c=pow(c,vec3(1.0/2.2));' +
  'gl_FragColor=vec4(c,1.0); }',
  { tB0: { value: null }, tB1: { value: null }, tB2: { value: null }, tB3: { value: null },
    w0: { value: 1 }, w1: { value: .72 }, w2: { value: .5 }, w3: { value: .34 },
    exposure: { value: qn('ex', 1.26) }, bloom: { value: qn('bloom', 1.0) }, time: { value: 0 } });
```

## Lighting

### Hemisphere Light

```javascript
scene.add(new THREE.HemisphereLight(0x31465e, 0x04070c, .55));
```

### Directional Light

```javascript
const key = new THREE.DirectionalLight(0x8fb0d0, .5);
key.position.set(30, 60, 20);
scene.add(key);
```

### Point Light

```javascript
const p1 = new THREE.PointLight(0xff3d7f, 4.2, 95, 1.8);
p1.position.set(NEST_X, 14.2, NEST_Z + 2);
scene.add(p1);
```
