---
theme: default
titleTemplate: "%s"
author: Karl Oskar Böhme
mdc: true
colorSchema: dark
progress: true

title: Stuxnet
transition: slide-left
class: text-center
hideInToc: true
---

<script setup>
import { vGlitch } from 'vue-powerglitch'

const glitch = {
  "timing": {
    "duration": 4000
  },
  "shake": {
    "velocity": 25,
    "amplitudeX": 0.2,
    "amplitudeY": 0.3
  },
}
</script>

<div v-glitch="glitch">

# STUXnet
von **Karl Oskar Böhme**, TIG 23

</div>

<style>
h1 {
    font-size: 10rem !important;
    line-height: 7.5rem !important;
}

.slidev-layout::before {
    content: "";
    position: absolute;
    inset: 0;
    background: linear-gradient(rgba(0, 0, 0, 0.333), rgba(0, 0, 0, 0.533)),
        url("https://t3.ftcdn.net/jpg/09/52/85/28/360_F_952852899_Tw352nYl4GOmcjuKz6k1w6qwd6IV3XIw.jpg") center/cover no-repeat;
    filter: blur(2px);
    z-index: -1;
}
</style>

<div class="scanlines"></div>

<style>
.scanlines {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: linear-gradient(
      rgba(18, 16, 16, 0) 50%, 
      rgba(0, 0, 0, 0.25) 50%
    ),
    linear-gradient(
      90deg, 
      rgba(255, 0, 0, 0.06), 
      rgba(0, 255, 0, 0.02), 
      rgba(0, 0, 255, 0.06)
    );
    background-size: 100% 10px, 2px 100%;
    z-index: 5;
    pointer-events: none;
}
</style>
