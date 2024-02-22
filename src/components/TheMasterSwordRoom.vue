<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import '../aframe/life-like-automaton.js';
import PortalTeleporter from './PortalTeleporter.vue';
</script>

<template>
    <a-entity gltf-model="#masterSwordRoom" rotation="0 0 0" position="0 0 -50" scale="0.1 0.1 0.1">
        <PortalTeleporter label="Return to main room" life-like-automaton="resolution: 256;" position="0 12 70"
            rotation="0 180 0" :rot="0" :y="0" :z="0" scale="10 10 10" />
    </a-entity>
    <ExitDoor />
</template>