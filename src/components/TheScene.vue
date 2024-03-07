<script setup>
import { ref } from 'vue';

import TheCameraRig from './TheCameraRig.vue';
import TheMainRoom from './TheMainRoom.vue';
import TheMasterSwordRoom from './TheMasterSwordRoom.vue';
import "../aframe/listen-to.js";
import "../aframe/bind-position.js";

defineProps({
  scale: Number,
  overlaySelector: String,
});

const allAssetsLoaded = ref(false);
</script>

<template>
  <a-scene background="color: black;" :webxr="`
      requiredFeatures: local-floor;
      referenceSpaceType: local-floor;
      optionalFeatures: dom-overlay;
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
      <a-asset-item id="wwWandItem" src="assets/ww_wand.glb"></a-asset-item>

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
      <a-asset-item id="templeOfTime" response-type="arraybuffer" src="assets/templeOfTime.mp3"
        preload="auto"></a-asset-item>
      <a-asset-item id="dekuSong" response-type="arraybuffer" src="assets/dekuSong.mp3" preload="auto"></a-asset-item>
      <a-asset-item id="goronSong" response-type="arraybuffer" src="assets/goronSong.mp3" preload="auto"></a-asset-item>
      <a-asset-item id="zoraSong" response-type="arraybuffer" src="assets/zoraSong.mp3" preload="auto"></a-asset-item>
      <a-asset-item id="error" response-type="arraybuffer" src="assets/OOT_Error.wav" preload="auto"></a-asset-item>
      <a-asset-item id="correct" response-type="arraybuffer" src="assets/OOT_Song_Correct.wav"
        preload="auto"></a-asset-item>
      <a-asset-item id="item" response-type="arraybuffer" src="assets/OOT_Fanfare_Item.wav"
        preload="auto"></a-asset-item>
    </a-assets>
    <template v-if="allAssetsLoaded">
      <TheMainRoom :scale="scale" />
      <TheMasterSwordRoom />
      <a-entity id="templeOfTimeTrigger" listen-to="target:a-scene; event:enter-scene; emit:backgroundSound"
        sound="src: #templeOfTime; loop:true; on:backgroundSound; volume:0.1"
        bind-position="target: #mainRoom"></a-entity>

      <a-entity id="noteD2" sound="src: #D2; on: start-D2; poolSize: 10"></a-entity>
      <a-entity id="noteD" sound="src: #D; on: start-D; poolSize: 10"></a-entity>
      <a-entity id="noteB" sound="src: #B; on: start-B; poolSize: 10"></a-entity>
      <a-entity id="noteA" sound="src: #A; on: start-A; poolSize: 10"></a-entity>
      <a-entity id="noteF" sound="src: #F; on: start-F; poolSize: 10"></a-entity>

      <a-entity id="dekuSongTrigger" sound="src: #dekuSong; on: start-dekuSound"
        bind-position="target: #dekuSongPart"></a-entity>
      <a-entity id="goronSongTrigger" sound="src: #goronSong; on: start-goronSound"
        bind-position="target: #goronSongPart"></a-entity>
      <a-entity id="zoraSongTrigger" sound="src: #zoraSong; on: start-zoraSound"
        bind-position="target: #zoraSongPart"></a-entity>
      <a-entity id="errorTrigger" sound="src: #error; on: start-errorSound"></a-entity>
      <a-entity id="correctTrigger" sound="src: #correct; on: start-correctSound"></a-entity>
    </template>
    <TheCameraRig />
  </a-scene>
</template>