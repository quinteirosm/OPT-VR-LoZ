<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import PortalTeleporter from './PortalTeleporter.vue';
import '../aframe/life-like-automaton.js';

defineProps({
  scale: Number,
});
</script>

<template>
  <a-entity gltf-model="#templeRoom" rotation="0 -180 0" position="0 0 -7">
    <PortalTeleporter material="src: #room-physic-texture" depth="0.1" position="0 1.76 9.691" rotation="0 180 0"
      scale="1.75 2.7 0.1" :rot="0" :y="0" :z="-19" :cameraEffect="true" :cameraY="1.70" :cameraZ="-17.6"
      :cameraRot="0" />
    <a-entity gltf-model="#deku" position="0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#goron" position="0 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#zora" position="-0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-box color="grey" depth="0.2" height="2.8" width="1.8" position="0 1.76 9.691"></a-box>
  </a-entity>
  <ExitDoor />
</template>