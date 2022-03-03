<template>
<div ref="canvasTest"></div>
</template>

<script setup lang="ts">
import { WebGLRenderer, PerspectiveCamera, Scene, BoxGeometry, MeshBasicMaterial, Mesh } from 'three'
import { ref, onMounted } from 'vue';
const canvasTest = ref<HTMLDivElement>()

const scene = new Scene();
const camera = new PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
onMounted(() => {
  if(canvasTest.value) {
    canvasTest.value.appendChild(renderer.domElement)
  }
})


const geometry1 = new BoxGeometry();
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
scene.add(cube3);

camera.position.z = 5;

function animate() {
  requestAnimationFrame(animate);
  cube1.rotation.x += 0.01;
  cube1.rotation.y += 0.01;
  cube2.rotation.x += 0.01;
  cube2.rotation.y += 0.01;
  cube3.rotation.x += 0.01;
  cube3.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();

// window.addEventListener('resize', () => {
//   renderer.setSize(window.innerWidth, window.innerHeight);
// })

</script>

<style scoped>

</style>
