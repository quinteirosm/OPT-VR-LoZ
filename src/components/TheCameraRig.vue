<script setup>
import '../aframe/disable-in-vr.js';
import '../aframe/hide-in-vr.js';
import '../aframe/simple-navmesh-constraint.js';
import '../aframe/blink-controls.js';
import '../aframe/physx-grab.js';
import { onMounted } from 'vue';

let notesPlayed = [];

const songDeku = ['D', 'D2', 'B', 'A', 'B', 'A'];
let songDekuPlayed = false;

const songGoron = ['F', 'D', 'F', 'D', 'A', 'F', 'A', 'F'];
let songGoronPlayed = false;

const songZora = ['D', 'F', 'A', 'A', 'B'];
let songZoraPlayed = false;

const compareArrays = (a, b) => {
  return JSON.stringify(a) === JSON.stringify(b);
};

function playedNote(note) {
  // only works if wwWand is has attribute data-grabbed
  if (!document.getElementById('wwWand').dataset.grabbed) {
    return;
  }

  document.getElementById(`note${note}`).emit(`start-${note}`);
  notesPlayed.push(note)

  if (notesPlayed.length == 5 && compareArrays(notesPlayed, songZora)) {
    document.getElementById('correctTrigger').emit('start-correctSound');
    document.getElementById('zoraSongTrigger').emit('start-zoraSound');
    document.querySelector('a-scene').emit('zoraPlayed');
    console.log('Zora song played');
    songZoraPlayed = true;

    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.getElementById('correctTrigger').emit('start-correctSound');
      document.querySelector('a-scene').emit('allSongsPlayed');
      notesPlayed = [];
    }
  }

  if (notesPlayed.length == 6 && compareArrays(notesPlayed, songDeku)) {
    document.getElementById('correctTrigger').emit('start-correctSound');
    document.getElementById('dekuSongTrigger').emit('start-dekuSound');
    document.querySelector('a-scene').emit('dekuPlayed');
    console.log('Deku song played');
    songDekuPlayed = true;

    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.getElementById('correctTrigger').emit('start-correctSound');
      document.querySelector('a-scene').emit('allSongsPlayed');
      notesPlayed = [];
    }
  }

  if (notesPlayed.length == 8 && compareArrays(notesPlayed, songGoron)) {
    document.getElementById('correctTrigger').emit('start-correctSound');
    document.getElementById('goronSongTrigger').emit('start-goronSound');
    document.querySelector('a-scene').emit('goronPlayed');
    console.log('Goron song played');
    songGoronPlayed = true;

    if (songDekuPlayed && songGoronPlayed && songZoraPlayed) {
      document.getElementById('correctTrigger').emit('start-correctSound');
      document.querySelector('a-scene').emit('allSongsPlayed');
      notesPlayed = [];
    }
  }

  if (notesPlayed.length > 8) {
    document.getElementById('errorTrigger').emit('start-errorSound');
    console.log('wrong song');
    notesPlayed = [];
  }
}

// songs
onMounted(() => {
  // For Desktop

  document.addEventListener("keypress", function (event) {
    if (event.key === "i") {
      playedNote('D2');
      console.log(notesPlayed);
    }
    if (event.key === "l") {
      playedNote('A');
      console.log(notesPlayed);
    }
    if (event.key === "k") {
      playedNote('F');
      console.log(notesPlayed);
    }
    if (event.key === "j") {
      playedNote('B');
      console.log(notesPlayed);
    }
    if (event.key === "u") {
      playedNote('D');
      console.log(notesPlayed);
    }
    if (event.key === "r") {
      document.getElementById('errorTrigger').emit('start-errorSound');
      notesPlayed = [];
      console.log(notesPlayed);
    }
  });

  // For VR
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
    playedNote('D');
    console.log(notesPlayed);
  });
});
</script>

<template>
  <a-entity id="camera-rig" movement-controls="camera: #head;" disable-in-vr="component: movement-controls;">

    <a-entity id="head" look-controls="pointerLockEnabled: true"
      simple-navmesh-constraint="navmesh: [data-role='nav-mesh']; height: 1.70;"
      disable-in-vr="component: simple-navmesh-constraint;" camera position="0 1.65 0">
      <a-entity id="ray" geometry="primitive: circle; radius: 0.0003;" material="shader: flat; color: white;" cursor
        raycaster="far: 2; objects: [clickable]; showLine: false;" position="0 0 -0.1"
        disable-in-vr="component: raycaster; disableInAR: false;" hide-in-vr="hideInAR: false">
        <a-entity id="dummy-hand-right" position="0.3 -0.4 -0.5"></a-entity>
        <a-entity id="dummy-hand-left" position="-0.3 -0.4 -0.5"></a-entity>
      </a-entity>

      <a-box width="3" height="2" depth="3" clickable id="music-alt-collider" position="-0.75 1.25 -2.2"
        scale="0.5 0.3 0.7" rotation="180 0 0" visible="false" physx-body="type: kinematic; emitCollisionEvents: true">
      </a-box>
      <a-box width="3" height="2" depth="3" clickable id="music-top-collider" position="0.75 1.25 -2.2"
        scale="0.5 0.3 0.7" rotation="180 0 0" visible="false" physx-body="type: kinematic; emitCollisionEvents: true">
      </a-box>
      <a-box width="4" height="2" depth="3" clickable id="music-down-collider" position="0 -1.25 -2.2"
        scale="0.5 0.3 0.7" rotation="180 0 0" visible="false" physx-body="type: kinematic; emitCollisionEvents: true">
      </a-box>
      <a-box width="3" height="2" depth="3" clickable id="music-left-collider" position="-1.4 0 -2.2"
        scale="0.5 0.3 0.7" rotation="180 0 90" visible="false" physx-body="type: kinematic; emitCollisionEvents: true">
      </a-box>
      <a-box width="3" height="2" depth="3" clickable id="music-right-collider" position="1.4 0 -2.2"
        scale="0.5 0.3 0.7" rotation="180 0 90" visible="false" physx-body="type: kinematic; emitCollisionEvents: true">
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
      raycaster="far: 2; objects: [clickable]; showLine: true;" physx-grab>
      <a-sphere id="hand-right-collider" radius="0.02" visible="false"
        physx-body="type: kinematic; emitCollisionEvents: true">
      </a-sphere>
    </a-entity>

  </a-entity>
</template>