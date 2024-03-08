<p align="center">
    <img src="triforce.png" alt="TriforceLogo" align="center"/>
</p>
<h1 align="center">The master sword trial - VR</h1>

![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)
![A-Frame](https://img.shields.io/badge/A%E2%80%93Frame-1.5-brightgreen?style=for-the-badge&labelColor=%23ef2d5e&color=%23ef2d5e)
![Threejs](https://img.shields.io/badge/threejs-black?style=for-the-badge&logo=three.js&logoColor=white)
![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)

### [>> DEMO <<](https://vr49.onivers.com/miguel/)

## Included in the project

### Movement modes support

- **Desktop** – Keyboard for move (_WASD_ or Arrows keys) + Mouse for look control (Drag and drop) + Keyboard for playing notes (_HJBNM_)
- **Mobile** – 1x Finger touch to go forward + 2x Fingers touch to go backward + Gaze cursor for click
- **VR Headset** – AR/VR walk + Teleport (Grip for grab and laser for click) + Gaze cursor for click

### Libs and components

- [**aframe-extras controls and animation-mixer**](https://github.com/c-frame/aframe-extras) \
  by [c-frame](https://github.com/c-frame) is licensed under [MIT License](https://github.com/c-frame/aframe-extras/blob/master/LICENSE)

- [**aframe physx**](https://github.com/c-frame/physx) \
  by [c-frame](https://github.com/c-frame) is licensed under [MIT License](https://github.com/c-frame/aframe-extras/blob/master/LICENSE)

- [**aframe-blink-controls**](https://github.com/jure/aframe-blink-controls/) \
  by [jure](https://github.com/jure) is licensed under [MIT License](https://github.com/jure/aframe-blink-controls/blob/main/LICENSE)

- [**simple-navmesh-constraint**](https://github.com/AdaRoseCannon/aframe-xr-boilerplate) \
  by [AdaRoseCannon](https://github.com/AdaRoseCannon) is licensed under [MIT License](https://github.com/AdaRoseCannon/aframe-xr-boilerplate/blob/glitch/LICENSE)

### 3D models

- [**Low-poly VR/Game Ready Interior Temple Scene**](https://skfb.ly/owIUD) \
  by [HermesAlvarado](https://sketchfab.com/HermesAlvarado) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

- [**Temple Of Time**](https://skfb.ly/6UVMx) \
  by [Jean-Sébastien Bass Galipeault](https://sketchfab.com/PomumCultor) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

- [**Kokiri's Emerald**](https://sketchfab.com/3d-models/kokiris-emerald-bd37124c71754f3099b4b3ebb8e83170) \
  by [brwntwn](https://sketchfab.com/brwntwn) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

- [**Goron's Ruby**](https://sketchfab.com/3d-models/goron-ruby-60cf0566cc7f4ac185891bfa625d76ae) \
  by [brwntwn](https://sketchfab.com/brwntwn) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

- [**Zora Sapphire**](https://sketchfab.com/3d-models/zora-sapphire-a98716a696ff4c4081c04ab39e90a5d2) \
  by [brwntwn](https://sketchfab.com/brwntwn) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

- [**Wind Waker | The Legend of Zelda: WW**](https://sketchfab.com/3d-models/wind-waker-the-legend-of-zelda-ww-685c477c40bb4fa991ce701d443f4ed9) \
  by [lumhax](https://sketchfab.com/lumhax") is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

  ### Audio

- [**Countdown**](https://opengameart.org/content/countdown) \
  by [qubodup](https://opengameart.org/users/qubodup) is licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) \
  Modifications: Added the files together in the following order: countdown-a, countdown-a, countdown-b.

### Image

- [**Les frères Mario**](https://www.favicon.cc/?action=icon&file_id=137640) \
  by [marcojetson](https://www.favicon.cc/?action=icon_list&user_id=36881) is licensed under [CC 0](https://creativecommons.org/publicdomain/zero/1.0/) \
  Modifications: Added a VR headset to Mario's head and two controllers.

---

## Quickstart

### Create a folder for your project and move to it

### Clone (or fork, or download)

```sh
git clone https://github.com/PatrickMarques24/mario-kart-shooter-vr.git
```

### Install dependencies

```sh
npm ci
```

### Dev

```sh
npm run dev
```

### Build

```sh
npm run build
```

## Notes for local dev on VR headset

1. Check that your development device and your VR headset are connected on **the same network**.

2. Expose you local development:

```sh
npm run dev-expose
```

3. In your VR headset, browse to the local development adress `[ip]:[port]`.

> [!NOTE]  
> The certificate is self-signed, so you will probably have to confirm access to the resource in your browser.

---

## License

![MIT License](https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge&color=%23262626)
