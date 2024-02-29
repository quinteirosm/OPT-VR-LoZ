<script setup>
import '../aframe/disable-in-vr.js';
import '../aframe/hide-in-vr.js';
import '../aframe/simple-navmesh-constraint.js';
import '../aframe/blink-controls.js';
import '../aframe/physx-grab.js';
import { onMounted } from 'vue';


// array stocking 5 notes
let notesPlayed = [];

//when notesPlayed contains five elements, compare it to the song
//if it matches, play the song
//if it doesn't, reset notesPlayed
const songDeku = [, 'D2', 'B', 'A', 'B', 'A'];
const songGoron = ['F', , 'F', , 'A', 'F', 'A', 'F'];
const songZora = [, 'F', 'A', 'A', 'B'];

function playedNote(note) {
  if (notesPlayed.length === 5) {
    if (notesPlayed === songDeku) {
      document.getElementById('dekuSong').play();
      console.log('Deku song played');
    } else if (notesPlayed === songGoron) {
      document.getElementById('goronSong').play();
      console.log('Goron song played');
    } else if (notesPlayed === songZora) {
      document.getElementById('zoraSong').play();
      console.log('Zora song played');
    } else {
      console.log('wrong song');
      notesPlayed = [];
    }
  } else {
    notesPlayed.push(note);
  }
}

// songs
onMounted(() => {
  document.querySelector('#music-top-collider').addEventListener('mouseenter', () => {
    playedNote('D2');
    console.log(notesPlayed);
  });

  document.querySelector('#music-right-collider').addEventListener('mouseenter', () => {
    playedNote('A');
    console.log(notesPlayed);
  });

  document.querySelector('#music-down-collider').addEventListener('mouseenter', () => {
    playedNote('F');
    console.log(notesPlayed);
  });

  document.querySelector('#music-left-collider').addEventListener('mouseenter', () => {
    playedNote('B');
    console.log(notesPlayed);
  });

  document.querySelector('#music-alt-collider').addEventListener('mouseenter', () => {
    notesPlayed.push('D');
    console.log(notesPlayed);
  });
});
</script>

<template>
  <a-entity id="camera-rig" movement-controls="camera: #head;" disable-in-vr="component: movement-controls;">

    <a-entity id="head" look-controls="pointerLockEnabled: true"
      simple-navmesh-constraint="navmesh: [data-role='nav-mesh']; height: 1.65;"
      disable-in-vr="component: simple-navmesh-constraint;" camera position="0 1.65 0">
      <a-entity geometry="primitive: circle; radius: 0.0003;" material="shader: flat; color: white;" cursor
        raycaster="far: 4; objects: [clickable]; showLine: false;" position="0 0 -0.1"
        disable-in-vr="component: raycaster; disableInAR: false;" hide-in-vr="hideInAR: false">
        <a-entity id="dummy-hand-right" position="0.3 -0.4 -0.5"></a-entity>
        <a-entity id="dummy-hand-left" position="-0.3 -0.4 -0.5"></a-entity>

        <a-plane clickable id="music-alt-collider" position="-0.05 0.05 0" scale="0.05 0.05 0.05" rotation="80 45 90"
          visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #D; on: mouseenter">
        </a-plane>
        <a-plane clickable id="music-top-collider" position="0.025 0.05 0" scale="0.05 0.05 0.05" rotation="80 0 0"
          visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #D2; on: mouseenter">
        </a-plane>
        <a-plane clickable id="music-down-collider" position="0.025 -0.05 0" scale="0.05 0.05 0.05" rotation="-80 0 0"
          visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #F; on: mouseenter">
        </a-plane>
        <a-plane clickable id="music-left-collider" position="-0.05 0 0" scale="0.05 0.05 0.05" rotation="0 80 0"
          visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #B; on: mouseenter">
        </a-plane>
        <a-plane clickable id="music-right-collider" position="0.1 0 0" scale="0.05 0.05 0.05" rotation="0 -80 0"
          visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #A; on: mouseenter">
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