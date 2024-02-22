<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import PortalTeleporter from './PortalTeleporter.vue';
import ExitDoor from './ExitDoor.vue';
import '../aframe/life-like-automaton.js';

defineProps({
  scale: Number,
});
</script>

<template>
  <a-entity gltf-model="#templeRoom" rotation="0 -180 0" position="0 0 -7">
    <PortalTeleporter label="Enter the Master Sword room" life-like-automaton="resolution: 256;" position="0 1.5 9.6"
      rotation="0 180 0" :rot="0" :y="0" :z="-45" />
    <a-entity gltf-model="#deku" position="0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#goron" position="0 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#zora" position="-0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
  </a-entity>
  <ExitDoor />
</template>