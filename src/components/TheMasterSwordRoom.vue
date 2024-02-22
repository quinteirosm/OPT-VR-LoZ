<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import '../aframe/life-like-automaton.js';
import PortalTeleporter from './PortalTeleporter.vue';
</script>

<template>
    <a-entity gltf-model="#masterSwordRoom" rotation="0 0 0" position="0 0.3 -24" scale="0.1 0.1 0.1">
        <a-entity gltf-model="#masterSword" position="0 16 0" scale="0.2 0.2 0.2" rotation="0 0 180"></a-entity>
    </a-entity>
    <ExitDoor />
</template>