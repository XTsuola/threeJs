<template>
  <input v-model="x" />
  <input v-model="y" />
  <input v-model="z" />
  <button @click="btn">点击我</button>

  <div ref="canvasTest"></div>
</template>

<script setup lang="ts">
import { WebGLRenderer, PerspectiveCamera, Scene, BoxGeometry, MeshBasicMaterial, Mesh, AmbientLight, } from 'three';
import { GLTFLoader, type GLTF } from "three/examples/jsm/loaders/GLTFLoader.js";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
import { ref, onMounted } from 'vue';

const canvasTest = ref<HTMLDivElement>()
const scene = new Scene();
const camera = new PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
onMounted(() => {
  if (canvasTest.value) {
    canvasTest.value.appendChild(renderer.domElement)
  }
})

const controls = new OrbitControls(camera, renderer.domElement);
const x = ref<number>(0)
const y = ref<number>(0)
const z = ref<number>(0)

function btn() {
  camera.position.set(x.value, y.value, z.value);
  controls.update();
}

/* const geometry1 = new BoxGeometry();
const material1 = new MeshBasicMaterial({ color: 0x00ffff });
const cube1 = new Mesh(geometry1, material1);
cube1.position.x = 2;
scene.add(cube1);

const geometry2 = new BoxGeometry();
const material2 = new MeshBasicMaterial({ color: 0xffff00 });
const cube2 = new Mesh(geometry2, material2);
cube2.position.x = -2;
scene.add(cube2);

const geometry3 = new BoxGeometry();
const material3 = new MeshBasicMaterial({ color: 0xff00ff });
const cube3 = new Mesh(geometry3, material3);
cube3.position.z = -5;
scene.add(cube3); */

camera.position.z = 5;

var loader = new GLTFLoader();
console.log(loader)
let test: GLTF | null = null
loader.load("/src/assets/Creeper.glb", function (gltf: GLTF) {
  test = gltf
  scene.add(gltf.scene);
})                                                                                            

var light = new AmbientLight(0xffffff);
scene.add(light);

function animate() {
  requestAnimationFrame(animate);
  /* cube1.rotation.x += 0.01;
  cube1.rotation.y += 0.01;
  cube2.rotation.x += 0.01;
  cube2.rotation.y += 0.01;
  cube3.rotation.x += 0.01;
  cube3.rotation.y += 0.01; */
  /* if(test) {
    test.scene.rotation.y += 0.1;
  } */
  controls.update();
  renderer.render(scene, camera);
}
animate();

// window.addEventListener('resize', () => {
//   renderer.setSize(window.innerWidth, window.innerHeight);
// })

</script>

<style scoped>
</style>
