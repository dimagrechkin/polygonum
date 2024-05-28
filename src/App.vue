<template>
  <div class="fullwidth">
    <Renderer
      ref="renderer"
      alpha
      :antialias="true"
      :pointer="{ onMove: onPointerMove }"
      resize
      :orbit-ctrl="{ enableDamping: true }"
    >
      <Camera :position="{ x: 0, y: 0, z: 25 }" />
      <Scene ref="scene">
        <!-- <FbxModel
        src="/src/components/models/ball.fbx"
        @load="onReady"
        @progress="onProgress"
        @error="onError"
      /> -->
        <!-- <Sphere
        :size="5"
        :position="{ x: 4, y: 4, z: 10 }"
        :rotation="{ x: 0, y: -1, z: 0 }"
        :scale="{ x: 1, y: 1, z: 1 }"
        castShadow
        receiveShadow
      >
        <StandardMaterial>
          <Texture src="/src/assets/soundcloud-logopng-28204.png" />
        </StandardMaterial>
      </Sphere> -->
        <!-- <,
TorusTroiPlane
        ref="avatar"
        :size="2000"
        :position="{ x: -4, y: 4, z: 5 }"
        :rotation="{ x: 0, y: 0, z: 0 }"
        :scale="{ x: 3, y: 3, z: 1 }"
      >
        <BasicMaterial>
          <Texture src="/src/assets/IMG_4507.jpg" />
        </BasicMaterial>
      </TroiPlane> -->
        <Sphere
          ref="soundcloud"
          :position="{ x: 0, y: 9, z: 1 }"
          :rotation="{ x: 0, y: 0, z: 0 }"
          :scale="{ x: 1, y: 1, z: 1 }"
          castShadow
          receiveShadow
          @click="testClick"
        >
          <BasicMaterial>
            <Texture :src="imgUrl" />
          </BasicMaterial>
        </Sphere>
        <!-- <Torus
          ref="youtube"
          :position="{ x: -5, y: 3, z: 0 }"
          :rotation="{ x: 0, y: -2, z: 0 }"
          :scale="{ x: 1.8, y: 1.8, z: 1.8 }"
          castShadow
          receiveShadow
          @click="testClick2"
        >
          <BasicMaterial>
            <Texture :src="imgYoutube" />
          </BasicMaterial>
        </Torus> -->
        <EffectComposer>
          <FilmPass />
          <UnrealBloomPass :strength="1" />
          <Text
            text="POLYGONUM"
            :font-src="textFont"
            align="center"
            :size="textMesh"
            :height="0.4"
            :position="{ x: 0, y: 6, z: 0 }"
          >
          </Text>
          <Text
            text="FRIDAY 9PM"
            :font-src="textFont"
            align="center"
            :size="textMesh"
            :height="0.4"
            :position="{ x: 0, y: 0, z: 0 }"
          >
          </Text>

          <Text
            text="location"
            :font-src="textFont"
            align="center"
            :size="textMesh"
            :height="0.7"
            :position="{ x: 0, y: -3, z: -1 }"
            @click="testClick3"
          >
          </Text>
        </EffectComposer>
        <!-- <AmbientLight /> -->
        <PointLight :color="light1Color" :position="{ x: 50, y: 50, z: 50 }" />
        <PointLight :color="light2Color" :position="{ x: -50, y: 50, z: 50 }" />
        <PointLight
          :color="light3Color"
          :position="{ x: -50, y: -50, z: 50 }"
        />
        <PointLight :color="light4Color" :position="{ x: 50, y: -50, z: 50 }" />

        <LiquidPlane
          ref="liquid"
          :width="WIDTH"
          :height="HEIGHT"
          :width-segments="512"
          :height-segments="512"
          :color="color"
          :metalness="metalness"
          :roughness="roughness"
        />
      </Scene>
      <EffectComposer>
        <!-- <FilmPass /> -->
        <RenderPass />
        <!-- <SMAAPass /> -->
        <!-- <UnrealBloomPass :strength="0.01" /> -->
        <!-- <HalftonePass :radius="1" :scatter="0" /> -->
      </EffectComposer>
    </Renderer>
  </div>

  <!-- <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/loveMusic.png"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="Polygonum" />

      <nav>
        <RouterLink to="/">Soma</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView /> -->
</template>
<script>
import { HelvetikerUtil } from "@/components/HelvetikerUtils";
import { Plane, Raycaster, Vector3 } from "three";
import { FontLoader } from "three/examples/jsm/loaders/FontLoader";

import imgUrl from "@/assets/soundcloud-logopng-28204.png";
import imgYoutube from "@/assets/youtube-logo-png-2069.png";
import textFont from "@/fonts/Bagoss_Standard_TRIAL_Regular_2?url";

import chroma from "chroma-js";
import {
  AmbientLight,
  Camera,
  PointLight,
  Renderer,
  Scene,
  Text,
  Sphere,
  Torus,
  Texture,
  EffectComposer,
  RenderPass,
  UnrealBloomPass,
  Plane as TroiPlane,
  BasicMaterial,
  FXAAPass,
  SMAAPass,
  FilmPass,
  HalftonePass,
} from "troisjs";
import LiquidPlane from "troisjs/src/components/liquid/LiquidPlane.js";
export default {
  components: {
    AmbientLight,
    Camera,
    LiquidPlane,
    PointLight,
    Renderer,
    Scene,
    Text,
    Sphere,
    SMAAPass,
    Texture,
    EffectComposer,
    RenderPass,
    UnrealBloomPass,
    FXAAPass,
    TroiPlane,
    FilmPass,
    BasicMaterial,
    HalftonePass,
    Torus,
  },
  setup() {
    return {
      WIDTH: 1080,
      HEIGHT: 1080,
      imgUrl,
      imgYoutube,
      textFont,
      // imgUrl: new URL("@/assets/soundcloud-logopng-28204.png", import.meta.url)
      //   .href,
    };
  },
  data() {
    return {
      color: "lightblue",
      metalness: 0.8,
      roughness: 0.2,
      light1Color: "#FFFF80",
      light2Color: "#DE3578",
      light3Color: "#FF4040",
      light4Color: "white",
      elemPosition: 1,
      textMesh: 1,
    };
  },
  mounted() {
    this.pointer = this.$refs.renderer.three.pointer;
    this.liquidEffect = this.$refs.liquid.liquidEffect;
    this.liquidEffect.addDrop(0, 0, 0.05, 0.05);
    // custom raycaster
    this.raycaster = new Raycaster();
    this.pointerPlane = new Plane(new Vector3(0, 0, 1), 0);
    this.pointerV3 = new Vector3();

    // const fontLoader = new FontLoader();
    // this.fontLoader.load(
    //   "node_modules/three/examples/fonts/droid/droid_serif_regular.typeface.json"
    // );

    const renderer = this.$refs.renderer;
    // const box = this.$refs.avatar.mesh;
    // renderer.onBeforeRender(() => {
    //   box.scale.y += 0.01;
    //   box.scale.x += 0.01;
    // });
    const myFont = new HelvetikerUtil();
    const FONTLoader = new FontLoader();
    this.font = FONTLoader.parse(myFont.data);

    const sphere = this.$refs.soundcloud.mesh;
    // const sphereYoutube = this.$refs.youtube.mesh;
    const textMesh = this.$refs.fontText;

    const x = window.matchMedia("(max-width: 700px)");

    renderer.onBeforeRender(() => {
      if (x.matches) {
        this.textMesh = 1;
      } else {
        this.textMesh = 3;
      }
      sphere.rotation.y += 0.01;
      // sphereYoutube.rotation.y += 0.07;
    });
  },

  methods: {
    testClick() {
      window.location.href = "https://soundcloud.com/user-286703045-278481029";
    },
    testClick2() {
      window.location.href = "https://www.youtube.com/watch?v=LtoxIgVJ-IM";
    },
    testClick3() {
      window.location.href =
        "https://maps.app.goo.gl/GywBFjk321UQQaYS8?g_st=ic";
    },
    onPointerMove() {
      this.raycaster.setFromCamera(
        this.pointer.positionN,
        this.$refs.renderer.three.camera
      );
      this.raycaster.ray.intersectPlane(this.pointerPlane, this.pointerV3);
      const x = (2 * this.pointerV3.x) / this.WIDTH;
      const y = (2 * this.pointerV3.y) / this.HEIGHT;
      this.liquidEffect.addDrop(x, y, 0.025, 0.005);
    },
    randomColors() {
      this.light1Color = chroma.random().hex();
      this.light2Color = chroma.random().hex();
      this.light3Color = chroma.random().hex();
      this.light4Color = chroma.random().hex();
    },
  },
};
</script>

<style scoped>
.fullwidth {
  width: 100%;
  min-height: 1024px;
}
body {
  margin: 0px;
  padding: 0px;
  min-height: 100%;
}
/* header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: white;
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
    margin-bottom: 40px;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
} */
</style>
