<template>
  <canvas id="canvas" width="600" height="400"></canvas>
</template>

<script>
import * as THREE from "three";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
// import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

export default {
  name: "RotateBox",
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
    const loader = new GLTFLoader();
    const model1 = null;
    const model2 = null;
    const model3 = null;
    const model4 = null;
    const model5 = null;
    // const controls = null;

    const angle = 0;
    const angle1 = 0;
    const angle2 = 0;
    const angle3 = 0;
    const random1 = Math.random() * 360;
    const random2 = Math.random() * 360;
    const random3 = Math.random() * 360;
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      cube,
      loader,
      model1,
      model2,
      model3,
      model4,
      model5,
      // controls,
      angle,
      angle1,
      angle2,
      angle3,
      random1,
      random2,
      random3
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
    this.renderer.setSize(window.innerWidth, window.innerHeight); // 画面の大きさを設定
    this.renderer.setClearColor(0xa95c0ec, 1);

    this.camera.position.set(0, 2, 15);
    this.light.position.set(0, 70, 30);
    // this.scene.add(this.cube);
    this.scene.add(this.light);
    this.loadModel1("model/school.glb", 50);
    this.loadModel2("model/zoom.glb", 40);
    this.loadModel3("model/cloud.glb", 1);
    this.loadModel4("model/cloud.glb", 4);
    this.loadModel5("model/cloud.glb", 2);
    // this.controls = new OrbitControls(this.camera, this.renderer.domElement);
    // this.controls.update();
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
    },
    loadModel1(filePath, scale) {
      this.loader.load(
        filePath,
        obj => {
          this.model1 = obj.scene;

          this.model1.scale.set(scale, scale, scale);
          this.scene.add(this.model1);
        }
        // function(xhr) {
        //   console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        // },
        // function(error) {
        //   console.error(error);
        // }
      );
    },
    loadModel2(filePath, scale) {
      this.loader.load(
        filePath,
        obj => {
          this.model2 = obj.scene;
          this.modelAnimate2();
          this.model2.scale.set(scale, scale, scale);
          this.scene.add(this.model2);
        }
        // function(xhr) {
        //   console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        // },
        // function(error) {
        //   console.error(error);
        // }
      );
    },
    loadModel3(filePath, scale) {
      this.loader.load(
        filePath,
        obj => {
          this.model3 = obj.scene;
          this.modelAnimate3();
          this.model3.scale.set(scale, scale, scale);
          this.scene.add(this.model3);
        }
        // function(xhr) {
        //   console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        // },
        // function(error) {
        //   console.error(error);
        // }
      );
    },
    loadModel4(filePath, scale) {
      this.loader.load(
        filePath,
        obj => {
          this.model4 = obj.scene;
          this.modelAnimate4();
          this.model4.scale.set(scale, scale, scale);
          this.scene.add(this.model4);
        }
        // function(xhr) {
        //   console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        // },
        // function(error) {
        //   console.error(error);
        // }
      );
    },
    loadModel5(filePath, scale) {
      this.loader.load(
        filePath,
        obj => {
          this.model5 = obj.scene;
          this.modelAnimate5();
          this.model5.scale.set(scale, scale, scale);
          this.scene.add(this.model5);
        }
        // function(xhr) {
        //   console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        // },
        // function(error) {
        //   console.error(error);
        // }
      );
    },
    modelAnimate2() {
      requestAnimationFrame(this.modelAnimate2);

      let y = Math.sin(this.angle) / 5 + 0.4;
      // console.log(y);

      //p
      this.model2.position.x = 3;
      this.model2.position.y = y;
      this.model2.position.z = 5;

      //ここにアニメーション用の変数更新を書く
      this.angle += 0.03;
    },
    modelAnimate3() {
      requestAnimationFrame(this.modelAnimate3);

      let x = Math.sin(this.angle1 + this.random1) * 15;
      let z = Math.cos(this.angle1 + this.random1) * 15;
      // console.log(y);

      //p
      this.model3.position.x = x;
      this.model3.position.y = 10;
      this.model3.position.z = z;

      //ここにアニメーション用の変数更新を書く
      this.angle1 += 0.004;
      console.log(`angle2 : ${this.angle2}`);
    },
    modelAnimate4() {
      requestAnimationFrame(this.modelAnimate4);

      let x = Math.sin(this.angle2 + this.random2) * 15;
      let z = Math.cos(this.angle2 + this.random2) * 15;
      // console.log(y);

      //p
      this.model4.position.x = x;
      this.model4.position.y = 10;
      this.model4.position.z = z;
      this.model4.rotation.y = 180;

      //ここにアニメーション用の変数更新を書く
      this.angle2 += 0.001;
    },
    modelAnimate5() {
      requestAnimationFrame(this.modelAnimate5);

      let x = Math.sin(this.angle3 + this.random3) * 15;
      let z = Math.cos(this.angle3 + this.random3) * 15;
      // console.log(y);

      //p
      this.model5.position.x = x;
      this.model5.position.y = 10;
      this.model5.position.z = z;

      //ここにアニメーション用の変数更新を書く
      this.angle3 += 0.002;
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