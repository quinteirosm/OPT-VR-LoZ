<script setup>
import '../aframe/disable-in-vr.js';
import '../aframe/hide-in-vr.js';
import '../aframe/simple-navmesh-constraint.js';
import '../aframe/blink-controls.js';
import '../aframe/physx-grab.js';

// array stocking 5 notes
const notesPlayed = [];


</script>

<template>
  <a-entity id="camera-rig" movement-controls="camera: #head;" disable-in-vr="component: movement-controls;">

    <a-entity id="head" look-controls="pointerLockEnabled: true"
      simple-navmesh-constraint="navmesh: [data-role='nav-mesh']; height: 1.65;"
      disable-in-vr="component: simple-navmesh-constraint;" camera position="0 1.65 0">
      <a-entity geometry="primitive: circle; radius: 0.0003;" material="shader: flat; color: white;" cursor
        raycaster="far: 4; objects: [clickable]; showLine: false;" position="0 0 -0.1"
        disable-in-vr="component: raycaster; disableInAR: false;" hide-in-vr="hideInAR: false">
        <a-plane id="music-left-collider" position="-0.05 0 0" scale="0.05 0.05 0.05" rotation="0 80 0" visible="true"
          physx-body="type: kinematic; emitCollisionEvents: true">
        </a-plane>
        <a-plane id="music-right-collider" position="0.05 0 0" scale="0.05 0.05 0.05" rotation="0 -80 0" visible="true"
          physx-body="type: kinematic; emitCollisionEvents: true">
        </a-plane>
        <a-plane id="music-top-collider" position="0 0.05 0" scale="0.05 0.05 0.05" rotation="80 0 0" visible="true"
          physx-body="type: kinematic; emitCollisionEvents: true">
        </a-plane>
        <a-plane id="music-down-collider" position="0 -0.05 0" scale="0.05 0.05 0.05" rotation="-80 0 0" visible="true"
          physx-body="type: kinematic; emitCollisionEvents: true">
        </a-plane>
      </a-entity>
    </a-entity>

    <a-entity id="hand-left" hand-controls="hand: left" blink-controls="
          cameraRig: #camera-rig;
          teleportOrigin: #head;
          snapTurn: false;
        " physx-grab>
      <a-sphere id="hand-left-collider" radius="0.02" visible="false"
        physx-body="type: kinematic; emitCollisionEvents: true">
      </a-sphere>
    </a-entity>

    <a-entity id="hand-right" hand-controls="hand: right" laser-controls="hand: right"
      raycaster="far: 4; objects: [clickable]; showLine: true;" physx-grab>
      <a-sphere id="hand-right-collider" radius="0.02" visible="false"
        physx-body="type: kinematic; emitCollisionEvents: true">
      </a-sphere>
    </a-entity>

  </a-entity>
</template>