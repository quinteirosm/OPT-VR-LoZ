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

function grabTheThing(evt, type) {
  // if something already grabbed, switch it
  const el = evt.target;
  const grabbedEl = document.querySelector('[data-grabbed]');

  if (grabbedEl) {
    el.setAttribute('clickable');
    grabbedEl.removeAttribute('bind-position');
    grabbedEl.removeAttribute('bind-rotation');
    grabbelEd.setAttribute('rotation', '0 0 90')
    copyPosition(document.querySelector('#camera-rig'), grabbedEl);
    grabbedEl.dataset.grabbed;
    return;
  }

  if (el.sceneEl.is('vr-mode')) {
    el.setAttribute('bind-position', 'target: #hand-right');
    el.setAttribute('bind-rotation', 'target: #hand-right; convertToLocal: true');
    if (el.id === 'wwWand') {
      el.setAttribute('bind-position', 'target: #hand-right');
      el.setAttribute('bind-rotation', 'target: #hand-right; convertToLocal: true');
      document.getElementById('hand-right').setAttribute('raycaster', 'far:5; showLine: false;');
      el.removeAttribute('clickable');
    }
  } else {
    el.setAttribute('bind-position', 'target: #dummy-hand-right');
    el.setAttribute('bind-rotation', 'target: #dummy-hand-right; convertToLocal: true');
  }

  setTimeout(() => {
    el.dataset.grabbed = true;
  }, 10);

  if (el.id === 'wwWand') {
    document.getElementById('wandText').setAttribute('visible', 'false');
  }
}

window.addEventListener('click', (evt) => {
  const grabbedEl = document.querySelector('[data-grabbed]');
  if (grabbedEl) {
    grabbedEl.removeAttribute('bind-position');
    grabbedEl.removeAttribute('bind-rotation');
    grabbedEl.setAttribute('rotation', '90 0 0')
    copyPosition(document.querySelector('#camera-rig'), grabbedEl);
    delete grabbedEl.dataset.grabbed;
    return;
  }
});

document.querySelector('a-scene').addEventListener('dekuPlayed', () => {
  document.querySelector('#dekuGem').setAttribute("visible", "true");
});

document.querySelector('a-scene').addEventListener('goronPlayed', () => {
  document.querySelector('#goronGem').setAttribute("visible", "true");
});

document.querySelector('a-scene').addEventListener('zoraPlayed', () => {
  document.querySelector('#zoraGem').setAttribute("visible", "true");
});

//when all songs are played, open the door by animating in on Y axis
document.querySelector('a-scene').addEventListener('allSongsPlayed', () => {
  document.getElementById('mainDoor').setAttribute('animation', {
    property: 'position',
    to: '0 5.5 9.691',
    dur: 5000,
    easing: 'linear'
  });
  document.getElementById('mainDoor').components.sound.playSound();
  setTimeout(() => {
    document.getElementById('mainDoor').components.sound.stopSound();
  }, 5000);
}
);
</script>

<template>
  <a-entity id="mainRoom" gltf-model="#templeRoom" rotation="0 -180 0" position="0 0 -7">

    <a-text id="wandText" value="It's dangerous to go alone! Take this." position="0 2 -4" rotation="0 180 0"
      scale="0.5 0.5 0.5" color="white" align="center" width="1" wrap-count="16" side="double" visible="true">
    </a-text>
    <a-entity>
      <a-entity id="wwWand" clickable @click="evt => grabTheThing(evt)" gltf-model="#wwWandItem"
        scale="0.0025 0.0025 0.0025" position="0 1 -4" rotation="90 0 0">
      </a-entity>
    </a-entity>

    <a-entity id="dekuGem" gltf-model="#deku" position="0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"
      visible="false"></a-entity>
    <a-entity id="goronGem" gltf-model="#goron" position="0 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"
      visible="false"></a-entity>
    <a-entity id="zoraGem" gltf-model="#zora" position="-0.5 1.3 7.25" scale="0.1 0.1 0.1" rotation="0 180 0"
      visible="false"></a-entity>

    <a-box id="mainDoor" color="grey" depth="0.2" height="3.5" width="1.8" position="0 1.980 9.742"
      sound="src: #stoneDoorSound; loop:true; on:start-doorSound; volume:1"></a-box>

    <PortalTeleporter material="src: #room-physics-texture" depth="0.1" position="0 1.980 9.742" rotation="0 180 0"
      scale="1.75 3.13 0.1" :rot="0" :y="0" :z="-19" :cameraEffect="true" :cameraY="1.70" :cameraZ="-19" />

    <a-text id="dekuSongPart" value="Minuet of Forest ↖️⬆️⬅️➡️⬅️➡️" position="2.996 2 -1.5" rotation="0 -90 0"
      scale="0.5 0.5 0.5" color="white" align="center" width="1" wrap-count="16" side="double">
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 1 0"
        position="-0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 1 0"
        position="0 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 0 0"
        position="0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="-0.25 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 0 0"
        position="0 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="0.25 -0.5 0"></a-entity>
    </a-text>
    <a-text id="goronSongPart" value="Bolero of Fire ⬇️↖️⬇️↖️➡️⬇️➡️⬇️" position="2.996 2 1.5" rotation="0 -90 0"
      scale="0.5 0.5 0.5" color="white" align="center" width="1" wrap-count="14" side="double">
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 0 -1 0"
        position="-0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 1 0"
        position="0 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 0 -1 0"
        position="0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 1 0"
        position="-0.25 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="0 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 0 -1 0"
        position="0.25 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="-0.125 -0.75 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 0 -1 0"
        position="0.125 -0.75 0"></a-entity>
    </a-text>

    <a-text id="zoraSongPart" value="Serenade of Water ↖️⬇️➡️➡️⬅️" position="-2.999 2 -1.5" rotation="0 90 0"
      scale="0.5 0.5 0.5" color="white" align="center" width="1" wrap-count="17" side="double">
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 1 0"
        position="-0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 0 -1 0"
        position="0 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="0.25 -0.25 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: 1 0 0"
        position="-0.125 -0.5 0"></a-entity>
      <a-entity arrow="length:0.1; headLength:0.05; headWidth:0.15; color: white; direction: -1 0 0"
        position="0.125 -0.5 0"></a-entity>
    </a-text>
  </a-entity>
  <ExitDoor />
  <!-- Main room navigation mesh  -->
  <!-- <a-entity geometry="primitive: plane; height: 12.5; width: 11.5" position="0 0 -5.9" rotation="-90 0 0"
    data-role="nav-mesh" material="color: blue" visible="false"></a-entity>
  <a-entity geometry="primitive: plane; height: 3.5; width: 4.5" position="0 0.4 -14.7" rotation="-90 0 0"
    data-role="nav-mesh" material="color: blue" visible="false"></a-entity> -->
</template>