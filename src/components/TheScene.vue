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
      <a-asset-item id="wwWand" src="assets/ww_wand.glb"></a-asset-item>
      <a-asset-item id="A" response-type="arraybuffer" src="assets/OOT_Notes_Ocarina_A_short.wav"
        preload="auto"></a-asset-item>
      <a-asset-item id="B" response-type="arraybuffer" src="assets/OOT_Notes_Ocarina_B_short.wav"
        preload="auto"></a-asset-item>
      <a-asset-item id="D" response-type="arraybuffer" src="assets/OOT_Notes_Ocarina_D_short.wav"
        preload="auto"></a-asset-item>
      <a-asset-item id="D2" response-type="arraybuffer" src="assets/OOT_Notes_Ocarina_D2_short.wav"
        preload="auto"></a-asset-item>
      <a-asset-item id="F" response-type="arraybuffer" src="assets/OOT_Notes_Ocarina_F_short.wav"
        preload="auto"></a-asset-item>

    </a-assets>

    <template v-if="allAssetsLoaded">
      <TheMainRoom :scale="scale" />
      <TheMasterSwordRoom />
    </template>

    <TheCameraRig />

  </a-scene>
</template>