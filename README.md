<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Transformaciones 3D Interactivas</title>
  <style>
    body { 
      margin: 0; 
      overflow: hidden;
      background: linear-gradient(135deg, #141e30, #243b55);
      font-family: Arial, sans-serif;
    }

    .titulo {
      position: absolute;
      top: 20px;
      width: 100%;
      text-align: center;
    }

    .titulo h1 {
      margin: 0;
      font-size: 34px;
      color: #00ffcc;
      text-shadow: 0 0 10px #00ffcc;
    }

    .titulo p {
      margin: 5px 0 0 0;
      font-size: 16px;
      color: #ffffff;
      text-shadow: 0 0 5px #ffffff;
    }
  </style>
</head>
<body>

<!-- TITULO -->
<div class="titulo">
  <h1>TRANSFORMACIONES 3D</h1>
  <p>HECHO POR LUIS EDWIN FUENTES MARIN</p>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<script>
  // ESCENA
  const scene = new THREE.Scene();

  // CÁMARA
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  camera.position.z = 5;

  // RENDERIZADOR
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  // LUZ
  const light = new THREE.PointLight(0xffffff, 1);
  light.position.set(5, 5, 5);
  scene.add(light);

  // CUBO (COLOR MEJORADO)
  const geometry = new THREE.BoxGeometry(1.2, 1.2, 1.2);
  const material = new THREE.MeshStandardMaterial({
    color: 0x00ffcc,  // verde-azulado neón
    metalness: 0.6,
    roughness: 0.3
  });

  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);

  // CONTROLES
  window.addEventListener('keydown', (e) => {

    // TRASLACIÓN
    if (e.key === 'ArrowRight') cube.position.x += 0.2;
    if (e.key === 'ArrowLeft')  cube.position.x -= 0.2;
    if (e.key === 'ArrowUp')    cube.position.y += 0.2;
    if (e.key === 'ArrowDown')  cube.position.y -= 0.2;

    // ROTACIÓN
    if (e.key === 'x') cube.rotation.x += 0.2;
    if (e.key === 'y') cube.rotation.y += 0.2;

    // ESCALA
    if (e.key === '+') {
      cube.scale.x += 0.1;
      cube.scale.y += 0.1;
      cube.scale.z += 0.1;
    }

    if (e.key === '-') {
      cube.scale.x -= 0.1;
      cube.scale.y -= 0.1;
      cube.scale.z -= 0.1;
    }

  });

  // ANIMACIÓN
  function animate() {
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
  }

  animate();

  // RESPONSIVE
  window.addEventListener('resize', () => {
    renderer.setSize(window.innerWidth, window.innerHeight);
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
  });

</script>

</body>
</html>
