<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import PortalTeleporter from './PortalTeleporter.vue';
import '../aframe/life-like-automaton.js';
</script>

<template>
    <a-entity gltf-model="#masterSwordRoom" rotation="0 0 0" position="0 0 -25" scale="0.1 0.1 0.1">
        <PortalTeleporter material="src: #room-physic-texture" position="0 13 71.280" rotation="0 180 0" scale="29 27 0.1"
            :rot="180" :y="0" :z="-16" :cameraEffect="true" :cameraY="1.80" :cameraZ="-17" :cameraRot="0" />
        <a-entity gltf-model="#masterSword" position="0 16 0" scale="0.2 0.2 0.2" rotation="0 0 180"></a-entity>
    </a-entity>
    <ExitDoor />
</template>