<template>
  <div id="title">
    <span> My digital Twin</span>
  </div>
  <div id="bg" ref="base_container"></div>
  <div v-if="showDescription" id="description" ref="description">
    <p>Click Heart, Lungs, and Stomach to see more information!!!</p>
  </div>
</template>

<script setup lang="ts">
import * as Copper from "copper3d_visualisation";

import { getCurrentInstance, onMounted, ref, Ref } from "vue";

let showDescription: Ref<boolean> = ref(true);
let refs = null;
let appRenderer: Copper.copperRenderer;

let showDiv: HTMLDivElement;

onMounted(() => {
  let { $refs } = (getCurrentInstance() as any).proxy;
  refs = $refs;

  const bg: HTMLDivElement = refs.base_container;
  showDiv = refs.description;

  if (bg.clientWidth < 800) {
    setTimeout(() => {
      changeStatus();
    }, 3000);
  }

  appRenderer = new Copper.copperRenderer(bg, { guiOpen: true });

  loadModel("digital_latest.gltf", "test");

  appRenderer.animate();
});
function loadModel(url: string, name: string) {
  let meshName = "";
  let scene1 = appRenderer.getSceneByName(name) as Copper.copperScene;
  if (scene1 == undefined) {
    const scene = appRenderer.createScene(name) as Copper.copperScene;
    if (scene) {
      // const camera = appRenderer.gui?.addFolder("camera");
      // camera?.add(scene.camera.position, "x").max(2000).min(-2000).step(1);
      // camera?.add(scene.camera.position, "y").max(2000).min(-2000).step(1);
      // camera?.add(scene.camera.position, "z").max(2000).min(-2000).step(1);
      appRenderer.setCurrentScene(scene);
      scene.controls.rotateSpeed = 2.5;
      scene.controls.noPan = true;
      const funa = () => {
        // window.location.replace(
        //   "https://linkungao.github.io/medtech-heart-vue/model-heart"
        // );
        // console.log(meshName);
        // console.log(scene);

        switch (meshName) {
          case "whole-lung":
            window.location.href =
              "http://sites.bioeng.auckland.ac.nz/medtech/lungs";
            break;
          case "heart":
            window.location.href =
              "https://linkungao.github.io/medtech-heart/model-heart";
            break;
          case "whole-stomach_1":
            window.location.href =
              "https://sparc.science/datasets/136?type=dataset";
            break;
          default:
            break;
        }
        // window.location.href =
        //   "https://linkungao.github.io/medtech-heart-vue/model-heart";
        document.removeEventListener("click", funa);
      };

      const opt = ["skin_epidermis", "skin_epidermis_1"];
      scene.loadGltf(url, (content) => {
        scene.pickModel(
          content,
          (mesh) => {
            if (showDescription) {
              if (scene.camera.position.x !== 39 || mesh) {
                changeStatus();
              }
            }

            if (mesh) {
              meshName = mesh.name;
              document.addEventListener("click", funa);
            } else {
              document.removeEventListener("click", funa);
            }
          },
          opt
        );
      });
      scene.loadViewUrl("human_view.json");

      scene.updateBackground("#00467F", "#BA4482");
    }
    Copper.setHDRFilePath("venice_sunset_1k.hdr");
    appRenderer.updateEnvironment();
  } else {
    appRenderer.setCurrentScene(scene1);
  }
}

function changeStatus() {
  showDescription.value = false;
}
</script>

<style>
#title {
  font-family: "Raleway", sans-serif;
  font-size: 30px;
  color: rgba(255, 255, 255, 0.9);
  position: fixed;
  top: 50px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
#bg {
  width: 100vw;
  height: 100vh;
  /* border: 1px solid palevioletred; */
}
#description {
  width: 150px;
  height: 100px;
  z-index: 10px;
  padding: 30px;
  display: flex;
  background-color: rgba(0, 0, 0, 0.2);
  color: rgba(255, 255, 255, 0.9);
  justify-content: baseline;
  align-items: center;
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  position: fixed;
  top: 300px;
  left: 80px;
}
.btn {
  position: fixed;
  left: 0;
  top: 0;
}
button {
  cursor: pointer;
  margin: 10px;
}
</style>
