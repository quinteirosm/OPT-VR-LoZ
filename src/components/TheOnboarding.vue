<script setup>
import { ref } from 'vue';

defineProps({
  loaded: Boolean,
});

const showOnboarding = ref(true);

function enterScene() {
  showOnboarding.value = false;
  if (AFRAME.utils.device.checkHeadsetConnected() && !AFRAME.utils.device.isMobile()) {
    document.querySelector('a-scene').enterVR();
  }
  document.querySelector('a-scene').emit('enter-scene');
}
</script>

<template>
  <div id="onboarding" v-if="showOnboarding">
    <div>
      <h1>The master sword trial - VR</h1>
      <p v-if="!loaded">loading...</p>
      <button v-if="loaded" @click="enterScene()">Enter scene</button>
      <div class="licences">
        <section>
          <h4>Introduction</h4>
          <p>
            This is a VR experience based on "The Legend of Zelda: Ocarina of Time". It is a
            tribute to the original game and its fans. It is not an official game and it is not
            affiliated with Nintendo. It is a non-profit school project.
          </p>
          <p>
            In this game, you'll have to play the 3 songs to unlock the 3 gems. Once done, something wonderful will
            happen. :)
          </p>
          <p>
            This game was made by <a href="https://github.com/quinteirosm">Miguel Quinteiros.</a>
          </p>
        </section>
        <section>
          <h4>Movement modes support</h4>
          <ul>
            <li>
              Desktop – Keyboard for move (WASD or Arrows keys) + Mouse for look
              control (Drag and drop). To play music notes, use the keys:
              <ul>
                <li>Top Left -> H</li>
                <li>Top Right -> J</li>
                <li>Bottom Left -> B</li>
                <li>Down -> N</li>
                <li>Bottom Right -> M</li>
              </ul>
            </li>
            <li>
              Mobile – 1x Finger touch to go forward + 2x Fingers touch to go
              backward + Gaze cursor for click
            </li>
            <li>
              VR Headset – AR/VR walk + Teleport (Grip for grab and laser for
              click) + Gaze cursor for click
            </li>
          </ul>
        </section>
        <dt>
        <dt>
          <i>3D assets used</i>
        </dt>
        <dt>
          <a href="https://github.com/c-frame/aframe-extras" target="_blank">aframe-extras controls and
            animation-mixer</a>
        </dt>
        <dd>
          <a href="https://github.com/c-frame/aframe-extras/blob/master/LICENSE" target="_blank">MIT License</a>
        </dd>

        <dt>
          <a href="https://github.com/c-frame/physx" target="_blank">aframe physx</a>
        </dt>
        <dd>
          <a href="https://github.com/c-frame/aframe-extras/blob/master/LICENSE" target="_blank">MIT License</a>
        </dd>

        <dt>
          <a href="https://github.com/jure/aframe-blink-controls/" target="_blank">aframe-blink-controls</a>
        </dt>
        <dd>
          <a href="https://github.com/jure/aframe-blink-controls/blob/main/LICENSE" target="_blank">MIT License</a>
        </dd>

        <dt>
          <a href=" https://github.com/AdaRoseCannon/aframe-xr-boilerplate"
            target="_blank">simple-navmesh-constraint</a>
        </dt>
        <dd>
          By Ada Rose Cannon under MIT License
        </dd>

        <dt>
          <a href="https://skfb.ly/owIUD" target="_blank">Low-poly VR/Game Ready Interior Temple Scene</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/HermesAlvarado" target="_blank">HermesAlvarado</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <a href="https://skfb.ly/6UVMx" target="_blank">Temple of Time</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/PomumCultor" target="_blank">Jean-Sébastien Bass Galipeault</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <a href="https://sketchfab.com/3d-models/kokiris-emerald-bd37124c71754f3099b4b3ebb8e83170"
            target="_blank">Kokiri's Emerald model</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/brwntwn" target="_blank">brwntwn</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <a href="https://sketchfab.com/3d-models/goron-ruby-60cf0566cc7f4ac185891bfa625d76ae" target="_blank">Goron
            Ruby</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/brwntwn" target="_blank">brwntwn</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <a href="https://sketchfab.com/3d-models/zora-sapphire-a98716a696ff4c4081c04ab39e90a5d2" target="_blank">Zora
            Sapphire</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/brwntwn" target="_blank">brwntwn</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <a href="https://sketchfab.com/3d-models/wind-waker-the-legend-of-zelda-ww-685c477c40bb4fa991ce701d443f4ed9"
            target="_blank">
            Wind Waker | The Legend of Zelda: WW</a>
        </dt>
        <dd>
          by <a href="https://sketchfab.com/lumhax" target="_blank">Lumhax</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>

        <dt>
          <i>Audio assets used</i>
        </dt>

        <dt>
          <a href="https://www.youtube.com/watch?v=ov7nj5RArTs&ab_channel=VideoGamesMusic">Temple of Time</a>
        </dt>
        <dd>
          by <a href="https://www.youtube.com/@VideoGamesMusic_VGM">VideoGamesMusic</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://www.youtube.com/watch?v=2Ko2-HaHLs0&ab_channel=VideoGamesMusic">Minuet of Forest</a>
        </dt>
        <dd>
          by <a href="https://www.youtube.com/@VideoGamesMusic_VGM">VideoGamesMusic</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://www.youtube.com/watch?v=zzxQZnj7sjU&ab_channel=VideoGamesMusic">Bolero of Fire</a>
        </dt>
        <dd>
          by <a href="https://www.youtube.com/@VideoGamesMusic_VGM">VideoGamesMusic</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://www.youtube.com/watch?v=VprgK2FcadY&ab_channel=VideoGamesMusic">Serenade of Water</a>
        </dt>
        <dd>
          by <a href="https://www.youtube.com/@VideoGamesMusic_VGM">VideoGamesMusic</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://noproblo.dayjo.org/ZeldaSounds/OOT/#Instruments">Ocarina notes short (A, B, D, F, D2)</a>
        </dt>
        <dd>
          by <a href="https://www.ZeldaSounds.com">HelpTheWretched</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://noproblo.dayjo.org/ZeldaSounds/OOT/#Menus_etc">Correct song</a>
        </dt>
        <dd>
          by <a href="https://www.ZeldaSounds.com">HelpTheWretched</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://noproblo.dayjo.org/ZeldaSounds/OOT/#Weapons_and_Items">Fanfare Item</a>
        </dt>
        <dd>
          by <a href="https://www.ZeldaSounds.com">HelpTheWretched</a>
          from The Legend of Zelda: Ocarina of Time
        </dd>

        <dt>
          <a href="https://opengameart.org/content/stone-door">
            Stone Door
          </a>
        </dt>
        <dd>
          by <a href="https://opengameart.org/users/bonebrah">bonebrah</a>
          under <a href="https://creativecommons.org/publicdomain/zero/1.0/" target="_blank">CC BY 1.0</a>
        </dd>

        <dt>
          <i>Images used</i>
        </dt>

        <dt>
          <a href="https://icon-icons.com/icon/triforce/39449">
            Triforce Icon
          </a>
        </dt>
        <dd>
          by <a href="https://icon-icons.com/users/V0FlbpEtoH55fqnf9aoeQ/icon-sets/">Lorc, Delapouite & contributors</a>
          under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a>
        </dd>
        </dt>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-size: 1.5rem
}

a {
  color: #eee;
  text-decoration: none;
}

.licences {
  margin: 2rem 0;
  font-size: 1rem;
  text-align: left;
}

.licences dt {
  padding-top: 0.75rem;
  font-size: 0.9rem;
  font-weight: bold;
}

.licences dd {
  margin-left: 0;
  font-size: 0.8rem;
}

#onboarding {
  position: absolute;
  top: 0;
  left: 0;
  background-color: #333;
  color: #ccc;
  width: 100vw;
  height: 100vh;
  padding: 1rem;
  font-family: monospace;
  z-index: 10000;
  overflow: auto;
}

#onboarding>* {
  margin: 0 auto;
  max-width: 50rem;
  width: calc(100vw - 10rem);
  text-align: center;
  border-radius: 0.3rem;
  padding: 1rem;
  font-size: 1.3rem;
}

#onboarding button {
  font-size: 1.3rem;
  padding: 0.5rem 1rem;
  border-radius: 0.3rem;
  background-color: white;
  color: black;
  border: none;
  cursor: pointer;
}
</style>#onboarding li {
#onboarding li {
font-size: 1rem;
text-align: left;
}
