<script>
  import * as THREE from 'three';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  //import { AnimationMixer } from 'three';
  import { onMount, onDestroy } from 'svelte';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

  let scene, camera, renderer, group, controls;//, mixer;
  
  function init(){
    scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);
  // Crea los OrbitControls y asigna la cámara y el renderer
  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true;
  controls.dampingFactor = 0.05;
  controls.screenSpacePanning = false;
  controls.minDistance = 1;
  controls.maxDistance = 50;
  const gltfLoader = new GLTFLoader();
  gltfLoader.load('/models/1-1-dicloroeteno.glb', (gltf) => {
    const { scene: gltfScene, animations } = gltf;
    //mixer = new AnimationMixer(gltfScene);
    //console.log(animations);
    //mixer.clipAction(animations[2]).play();
    group = new THREE.Group();
    group.add(gltfScene);
    scene.add(group);
    const light = new THREE.PointLight(0xffffff, 1, 100);
    light.position.set(20, 20, 20);
    scene.add(light);
    //I need to add more light to the scene but in different positions
    const light2 = new THREE.PointLight(0xffffff, 1, 100);
    light2.position.set(-20, -20, -20);
    scene.add(light2);
    //I need to add more light to the scene but in different positions
    const light3 = new THREE.PointLight(0xffffff, 1, 100);
    light3.position.set(20, -20, 20);
    scene.add(light3);
    //I need to add more light to the scene but in different positions
    const light4 = new THREE.PointLight(0xffffff, 1, 100);
    light4.position.set(-20, 20, -20);
    scene.add(light4);
    //I need to add more light to the scene but in different positions
    const light5 = new THREE.PointLight(0xffffff, 1, 100);
    light5.position.set(20, 20, -20);
    camera.position.z = 15;
    camera.position.y = -1;
    camera.position.x = -1;
    // Inicia la animación en bucle
    renderer.setAnimationLoop( function () {
      //animate();
      renderer.render(scene, camera);
    } );
    
  });
}

/*function animate() {
  // Actualizar la animación si está disponible
  if (mixer) {
    mixer.update(0.01);
  }
}*/

onMount(() => {
  init();
});

  onDestroy(() => {
    if (group) {
      group.traverse((obj) => {
        if (obj.geometry) {
          obj.geometry.dispose();
          obj.geometry = undefined;
        }
        if (obj.material) {
          obj.material.dispose();
          obj.material = undefined;
        }
      });
    }
  });
  
</script>

<div >
  <group>
    <group
      name="NurbsPath001"
      position={[0, 1.8, -3.27]}
      rotation={[0, 1.33, 0]}
      scale={[1.44, 1, 1.03]}
    >
      <group
        name="Sphere003"
        position={[-2.61, -0.35, 0.76]}
        rotation={[-2.39, 0.03, -1.49]}
        scale={[0.98, 0.7, 0.98]}
      >
        <mesh
          name="Sphere006"
          castShadow
          receiveShadow
        >
          <bufferGeometry attach="geometry" />
          <meshStandardMaterial attach="material" />
        </mesh>
        <mesh
          name="Sphere006_1"
          castShadow
          receiveShadow
        >
          <bufferGeometry attach="geometry" />
          <meshStandardMaterial attach="material" />
        </mesh>
        <mesh
          name="Sphere006_2"
          castShadow
          receiveShadow
        >
          <bufferGeometry attach="geometry" />
          <meshStandardMaterial attach="material" />
        </mesh>
      </group>
    </group>
    <mesh
      name="Sphere"
      castShadow
      receiveShadow
      position={[0, -4.7, 0.26]}
      scale={2}
    >
      <bufferGeometry attach="geometry" />
      <meshStandardMaterial attach="material" />
    </mesh>
  </group>
</div>