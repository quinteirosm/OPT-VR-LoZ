<script setup>
import { ref } from 'vue';
import { randomHsl } from '../utils/color.js';
import PortalTeleporter from './PortalTeleporter.vue';
import '../aframe/life-like-automaton.js';
import { copyPosition, copyRotation } from '../utils/aframe.js';
import '../aframe/bind-position.js';
import '../aframe/bind-rotation.js';

defineProps({
    scale: Number,
});

function grabTheThing(evt) {
    // if something already grabbed, switch it
    const el = evt.target;
    const grabbedEl = document.querySelector('[data-grabbed]');
    if (grabbedEl) {
        grabbedEl.removeAttribute('bind-position');
        copyPosition(document.querySelector('#camera-rig'), grabbedEl);
        delete grabbedEl.dataset.grabbed;
        return;
    }

    if (el.sceneEl.is('vr-mode')) {
        el.setAttribute('bind-position', 'target: #hand-right');
        el.setAttribute('bind-rotation', 'target: #hand-right; convertToLocal: true');
    } else {
        el.setAttribute('bind-position', 'target: #dummy-hand-right');
        el.setAttribute('bind-rotation', 'target: #dummy-hand-right; convertToLocal: true');
    }
    setTimeout(() => {
        el.dataset.grabbed = true;
    }, 500);

    if (el.id === 'masterSwordObject') {
        el.components.sound.playSound();
        document.getElementById('swordText').setAttribute('visible', 'true');
    }
}


window.addEventListener('click', (evt) => {
    const grabbedEl = document.querySelector('[data-grabbed]');
    if (grabbedEl) {
        grabbedEl.removeAttribute('bind-position');
        grabbedEl.removeAttribute('bind-rotation');
        copyPosition(document.querySelector('#camera-rig'), grabbedEl);
        delete grabbedEl.dataset.grabbed;
        return;
    }
}
);

</script>

<template>
    <a-entity gltf-model="#masterSwordRoom" rotation="0 0 0" position="0 0 -25" scale="0.1 0.1 0.1">
        <PortalTeleporter material="src: #room-physic-texture" position="0 13 71.280" rotation="0 180 0"
            scale="29 27 0.1" :rot="180" :y="0" :z="-16.5" :cameraEffect="true" :cameraY="1.70" :cameraZ="-17"
            :cameraRot="0" />
        <a-text geometry="primitive:plane; width:5; height:3" material="side:double;color:black" id="swordText"
            value="Congratulations! You've became the Hero of Time!" position="0 16 0" rotation="0 0 0" color="white"
            align="center" wrap-count="16" side="double" visible="false">
        </a-text>
        <a-entity id="masterSwordObject" clickable @click="evt => grabTheThing(evt)" gltf-model="#masterSword"
            position="0 16 0" scale="0.2 0.2 0.2" rotation="0 0 180"
            sound="src: #item; loop:false; on:start-soundItem; volume:0.5">
        </a-entity>
    </a-entity>
    <ExitDoor />
    <!-- Main room navigation mesh -->
    <a-entity id="swordMesh" geometry="primitive: plane; height: 12; width: 12" position="0 0.2 -25" rotation="-90 0 0"
        data-role="nav-mesh" material="color: blue" visible="false"></a-entity>
    <a-entity id="swordAltarMesh" geometry="primitive: plane; height: 2; width: 2" position="0 0.5 -25"
        rotation="-90 0 0" data-role="nav-mesh" material="color: blue" visible="false"></a-entity>
</template>