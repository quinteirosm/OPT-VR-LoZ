<script setup>
import { ref } from 'vue';

import TheCameraRig from './TheCameraRig.vue';
import TheMainRoom from './TheMainRoom.vue';
import TheMasterSwordRoom from './TheMasterSwordRoom.vue';

defineProps({
  scale: Number,
  overlaySelector: String,
});

const allAssetsLoaded = ref(false);
</script>

<template>
  <a-scene stats background="color: black;" :webxr="`
      requiredFeatures: local-floor;
      referenceSpaceType: local-floor;
      optionalFeatures: dom-overlay;
      overlayElement: ${overlaySelector};
    `" xr-mode-ui="XRMode: xr" physx="
      autoLoad: true;
      delay: 1000;
      useDefaultScene: false;
      wasmUrl: lib/physx.release.wasm;
    ">

    <a-assets @loaded="allAssetsLoaded = true">
      <a-asset-item id="templeRoom" src="assets/temple_room.glb"></a-asset-item>
      <a-asset-item id="masterSwordRoom" src="assets/swordRoom.glb"></a-asset-item>
      <a-asset-item id="masterSword" src="assets/masterSword.glb"></a-asset-item>
      <a-asset-item id="deku" src="assets/deku_emerald.glb"></a-asset-item>
      <a-asset-item id="goron" src="assets/goron_ruby.glb"></a-asset-item>
      <a-asset-item id="zora" src="assets/zora_sapphire.glb"></a-asset-item>
      <a-asset-item id="sound-1" response-type="arraybuffer" src="assets/sound1.mp3" preload="auto"></a-asset-item>
    </a-assets>

    <template v-if="allAssetsLoaded">
      <TheMainRoom :scale="scale" />
      <TheLifeCubeRoom />
      <ThePhysicRoom />
      <TheMasterSwordRoom />
    </template>

    <TheCameraRig />

  </a-scene>
</template>