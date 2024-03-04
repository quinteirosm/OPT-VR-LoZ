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
    grabbedEl.removeAttribute('bind-rotation');
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
});

//when all songs are played, open the door by animating in on Y axis
document.querySelector('a-scene').addEventListener('allSongsPlayed', () => {
  document.getElementById('mainDoor').setAttribute('animation', {
    property: 'position',
    to: '0 10.76 9.691',
    dur: 20000,
    easing: 'linear'
  });
}
);
</script>

<template>
  <a-entity gltf-model="#templeRoom" rotation="0 -180 0" position="0 0 -7">
    <PortalTeleporter material="src: #room-physic-texture" depth="0.1" position="0 1.76 9.691" rotation="0 180 0"
      scale="1.75 2.7 0.1" :rot="0" :y="0" :z="-19" :cameraEffect="true" :cameraY="1.70" :cameraZ="-17.6"
      :cameraRot="0" />
    <a-entity clickable @click="evt => grabTheThing(evt)" gltf-model="#wwWand" scale="0.0025 0.0025 0.0025"
      position="0 1 1" rotation="0 0 180"></a-entity>
    <a-entity gltf-model="#deku" position="0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#goron" position="0 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-entity gltf-model="#zora" position="-0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"></a-entity>
    <a-box id="mainDoor" color="grey" depth="0.2" height="2.8" width="1.8" position="0 1.76 9.691"></a-box>
  </a-entity>
  <ExitDoor />
  <!-- Main room navigation mesh  -->
  <!-- <a-entity geometry="primitive: plane; height: 12.5; width: 11.5" position="0 0 -5.9" rotation="-90 0 0"
    data-role="nav-mesh" material="color: blue" visible="false"></a-entity>
  <a-entity geometry="primitive: plane; height: 3.5; width: 4.5" position="0 0.4 -14.7" rotation="-90 0 0"
    data-role="nav-mesh" material="color: blue" visible="false"></a-entity> -->
</template>