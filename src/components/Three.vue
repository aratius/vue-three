<template>
  <canvas id="canvas" width="600" height="400"></canvas>
</template>

<script>
import * as THREE from "three";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

export default {
  name: "Three",
  data() {
    const scene = new THREE.Scene();
    const renderer = null;
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    const light = new THREE.DirectionalLight(0xffffff, 2);
    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshNormalMaterial();
    const cube = new THREE.Mesh(geometry, material);
    const gltfLoader = new GLTFLoader();
    const fontLoader = new THREE.FontLoader();
    const controls = null;
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      cube,
      gltfLoader,
      fontLoader,
      controls
    };
  },
  mounted() {
    window.addEventListener("resize", this.resize);

    const $canvas = document.getElementById("canvas");
    // canvasを後付けで設定する方法あったら教えてほしいー
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      canvas: $canvas
    });

    this.controls = new OrbitControls(this.camera, $canvas);
    this.renderer.setSize(window.innerWidth, window.innerHeight); // 画面の大きさを設定
    this.renderer.setClearColor(0xa95c0ec, 1);

    this.camera.position.set(0, 0, 2);
    this.light.position.set(0, 70, 30);
    this.scene.add(this.cube);
    this.scene.add(this.light);
    this.animate();
  },
  methods: {
    animate() {
      requestAnimationFrame(this.animate);

      this.cube.rotation.x += 0.02;
      this.cube.rotation.y += 0.02;

      this.renderer.render(this.scene, this.camera);
    },
    resize() {
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);

      // カメラのアスペクト比を正す
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
    }
  }
};
</script>

<style>
#canvas {
  width: 100%;
  height: 100%;
  margin: 0;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: -1;
}
</style>