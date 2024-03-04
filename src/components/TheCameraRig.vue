<script setup>
import '../aframe/disable-in-vr.js';
import '../aframe/hide-in-vr.js';
import '../aframe/simple-navmesh-constraint.js';
import '../aframe/blink-controls.js';
import '../aframe/physx-grab.js';
import { onMounted } from 'vue';


// array stocking 5 notes
let notesPlayed = [];

// a,t,l,r,l,r
const songDeku = ['D', 'D2', 'B', 'A', 'B', 'A'];
let songDekuPlayed = false;
// d,a,d,a,r,d,r,d
const songGoron = ['F', 'D', 'F', 'D', 'A', 'F', 'A', 'F'];
let songGoronPlayed = false;
// a,d,r,r,l
const songZora = ['D', 'F', 'A', 'A', 'B'];
let songZoraPlayed = false;

const compareArrays = (a, b) => {
  return JSON.stringify(a) === JSON.stringify(b);
};

function playedNote(note) {
  notesPlayed.push(note);
  if (notesPlayed.length == 5 && compareArrays(notesPlayed, songZora)) {
    document.getElementById('zoraSongTrigger').emit('start-zoraSound');
    console.log('Zora song played');
    songZoraPlayed = true;
    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.querySelector('a-scene').emit('allSongsPlayed');
    }
    notesPlayed = [];
  }
  if (notesPlayed.length == 6 && compareArrays(notesPlayed, songDeku)) {
    document.getElementById('dekuSongTrigger').emit('start-dekuSound');
    console.log('Deku song played');
    songDekuPlayed = true;
    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.querySelector('a-scene').emit('allSongsPlayed');
    }
    notesPlayed = [];
  }
  if (notesPlayed.length == 8 && compareArrays(notesPlayed, songGoron)) {
    document.getElementById('goronSongTrigger').emit('start-goronSound');
    console.log('Goron song played');
    songGoronPlayed = true;
    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.querySelector('a-scene').emit('allSongsPlayed');
    }
    notesPlayed = [];
  }
  if (notesPlayed.length > 8) {
    document.getElementById('errorTrigger').emit('start-errorSound');
    console.log('wrong song');
    notesPlayed = [];
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
      simple-navmesh-constraint="navmesh: [data-role='nav-mesh']; height: 1.70;"
      disable-in-vr="component: simple-navmesh-constraint;" camera position="0 1.65 0">
      <a-entity geometry="primitive: circle; radius: 0.0003;" material="shader: flat; color: white;" cursor
        raycaster="far: 4; objects: [clickable]; showLine: false;" position="0 0 -0.1"
        disable-in-vr="component: raycaster; disableInAR: false;" hide-in-vr="hideInAR: false">
        <a-entity id="dummy-hand-right" position="0.3 -0.4 -0.5"></a-entity>
        <a-entity id="dummy-hand-left" position="-0.3 -0.4 -0.5"></a-entity>
      </a-entity>

      <a-box width="3" height="2" clickable id="music-alt-collider" position="-0.5 1 -1.2" scale="0.3 0.3 0.3"
        rotation="0" visible="true" physx-body="type: kinematic; emitCollisionEvents: true"
        sound="src: #D; on: mouseenter">
      </a-box>
      <a-box width="3" height="2" clickable id="music-top-collider" position="0.75 1 -1.2" scale="0.3 0.3 0.3"
        rotation="0" visible="true" physx-body="type: kinematic; emitCollisionEvents: true"
        sound="src: #D2; on: mouseenter">
      </a-box>
      <a-box width="3" height="2" clickable id="music-down-collider" position="0.75 -1 -1.2" scale="0.3 0.3 0.3"
        rotation="0" visible="true" physx-body="type: kinematic; emitCollisionEvents: true"
        sound="src: #F; on: mouseenter">
      </a-box>
      <a-box width="3" height="2" clickable id="music-left-collider" position="-0.75 0 -1.2" scale="0.3 0.3 0.3"
        rotation="0" visible="true" physx-body="type: kinematic; emitCollisionEvents: true"
        sound="src: #B; on: mouseenter">
      </a-box>
      <a-box width="3" height="2" clickable id="music-right-collider" position="2 0 -1.2" scale="0.3 0.3 0.3" rotation="0"
        visible="true" physx-body="type: kinematic; emitCollisionEvents: true" sound="src: #A; on: mouseenter">
      </a-box>
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