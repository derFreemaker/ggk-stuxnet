---
theme: seriph
titleTemplate: "%s"
author: Karl Oskar Böhme
colorSchema: dark
mdc: true
progress: true

title: Stuxnet
transition: slide-up
class: text-center
hideInToc: true
---

<script setup>
import { vGlitch } from 'vue-powerglitch'

const glitch = {
  "timing": {
    "duration": 10000
  },
  "shake": {
    "velocity": 10,
    "amplitudeX": 0.2,
    "amplitudeY": 0.2,
  },
  "glitchTimeSpan": {
    "start": 0.1,
    "end": 0.4,
  }
}
</script>

<div v-glitch="glitch">

# STUXnet
###### von **Karl Oskar Böhme**, TIG 23

</div>

<style>
h1 {
  font-size: 10rem !important;
  line-height: 10rem !important;
}

.slidev-layout::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(rgba(0, 0, 0, 0.333), rgba(0, 0, 0, 0.533)),
      url("https://t3.ftcdn.net/jpg/09/52/85/28/360_F_952852899_Tw352nYl4GOmcjuKz6k1w6qwd6IV3XIw.jpg") center/cover no-repeat;
  filter: blur(2px);
  z-index: -10;
}
</style>

---
transition: slide-left
layout: image-right
image: https://www.it-daily.net/images/Aufmacher-2019/Security_Operations_Center_shutterstock_669226159_700.jpg
level: 2
---

<LocationBanner >

**Juni 2010** in Minsk (Belarus)

</LocationBanner>

# Entdeckung

Eine IT-Sicherheitsunternehmen untersucht dauernd abstürzende Computer von einem iranischen Kunden.
<br>
<br>

<div v-click="1">

## Ihr Fund:

</div>
<br>

<div
  v-click="1"
  v-motion
    :initial="{ x: 50, y: 50 }"
    :enter="{ x: 0, y: 100 }"
    :click-2="{ y: 25 }"
    :click-3="{ y: 0 }"
>

> **vielfaches größer und komplexer** als normale Malware,
> ~600KB statt wie Conficker mit ~35KB

</div>
<br>

<div
  v-click="2"
  v-motion
    :initial="{ x: -50, y: 100 }"
    :enter="{ x: 0, y: 25 }"
    :click-3="{ y: 0 }"
>

> **keine** Ransomware, Botnetz-Virus, oder ...

</div>
<br>

<div
  v-click="3"
  v-motion
    :initial="{ x: -100, y: 0 }"
    :enter="{ x: 0, y: 0 }"
>

> **speziell abgestimmt** auf sein Ziel

</div>
<br>

---
transition: slide-down
---

<script setup>
import { LineSquiggle, CircuitBoard, ClockFading, Factory, BrickWallFire } from 'lucide-vue-next';
</script>

# Was ist STUXnet?

<div class="text-gray-400"
  v-click="1">

Ist ein Wurm<span v-click="1" v-motion :initial="{ opacity: 0 }" :enter="{ opacity: 1, transition: { delay: 1000, duration: 100 } }">, eine Malware welche sich von alleine automatisch ausbreitet.</span>
</div>
<br>

<div v-click="2">

**Was macht ihn dann besonders?**
</div>

<div class="mt-6 grid grid-cols-2 gap-8 px-8 text-center">

<div class="feature-box items-center"
  v-click="3"
  v-motion
    :initial="{ x: '100%', y: '50%', scale: 1.5 }"
    :enter="{ x: '50%' }"
      :click-4="{ x: '0%', y: '0%', scale: 1 }">
  <CircuitBoard class="mb-4" size="36" />
  <div class="text-sm text-gray-400">
  
ungewöhnlich groß und komplex, mit einer Größe von **~600KB**
  </div>
</div>

<div class="feature-box items-center"
  v-click="4"
  v-motion
    :initial="{ x: '50%', y: '200%', scale: 1.2 }"
    :enter="{ x: '-25%', y: '50%' }"
      :click-5="{ x: '0%', y: '0%', scale: 1 }">
  <ClockFading class="mb-4" size="36" />
  <div class="text-sm text-gray-400">

Entwicklungszeit von **2-3 Jahren** mit einem Team von **10 Personen**
  </div> 
</div>

<div class="feature-box items-center"
  v-click="5"
  v-motion
    :initial="{ x: -100 }"
    :enter="{ x: 0 }">
  <Factory class="mb-4" size="36"/>
  <div class="text-sm text-gray-400">

erste bekannter digitaler Angriff auf **industrielle Infrastruktur**
  </div>
</div>

<div class="feature-box items-center"
  v-click="6"
  v-motion
    :initial="{ y: 100 }"
    :enter="{ y: 0 }">
  <BrickWallFire class="mb-4" size="36" />
  <div class="text-sm text-gray-400">

verwendete **gestohlene Zertifikate**,<br> und **<span class="font-bold" v-mark.underline.orange="7">4 Zero-Days</span>**
  </div>
</div>

</div>
<br>


---
transition: slide-up
---

<script setup>
import { HatGlasses, DollarSign } from 'lucide-vue-next';
</script>

<div class="mt-8 text-center">

## Was ist ein "Zero-Day"?
<div class="text-sm text-gray-400">
(Sicherheitslücke)
</div>

</div>
<br>

<div class="grid grid-cols-2 gap-8 mt-12 px-8 text-center">
  
<div class="feature-box items-center"
  v-click="1"
  v-motion
    :initial="{ x: 100, y: 200, scale: 1.2 }"
    :enter="{ x: 50, y: 0 }"
      :click-2="{ x: 0, scale: 1 }">
  <HatGlasses class="mb-4 text-color-[--slidev-theme-primary]" size="48" />
  <div class="font-bold text-xl mb-2">perfekte Tarnung</div>
  <div class="text-sm text-gray-400">

Ist eine **unbekannte** Sicherheitslücke, und somit haben Entwickler **0 Tage** um sie zu beheben.
  </div>
</div>
  
<div class="feature-box items-center"
  v-click="2"
  v-motion
    :initial="{ x: 200 }"
    :enter="{ x: 0 }">
  <DollarSign class="mb-4 text-color-[--slidev-theme-primary]" size="48" />
  <div class="font-bold text-xl mb-2">extrem Wertvoll</div>
  <div class="text-sm text-gray-400">

Einen "Zero-Day" zu kennen wird als **glücklich** bezeichnet.
  </div>
</div>

</div>

---
transition: slide-left
---

# Wofür wurde STUXnet entwickelt?

<div class="mt-12 h-full timeline-window" v-click>
<div class="timeline"
  v-motion
    :initial="{ y: '0%' }"
    :click-5="{ y: '-33.3%' }">

<div class="timeline-node" v-click="[1, 5]">
  <div class="mb-4">2002</div>
  <div class="feature-box">

### Aufdeckung von Nuklearanlagen
<span class="text-sm text-gray-400">Eine iranische Wiederstandsgruppe deckt zwei unbekannte iranische Nuklearanlagen auf.</span>
  </div>
</div>

<div class="timeline-node" v-click="4">
  <div class="mb-4">SOME DATE 2</div>
  <div class="feature-box">

### Foo 2
<span class="text-sm text-gray-400">TODO...</span>
  </div>
</div>

<div class="timeline-node" v-click="5">
  <div class="mb-4">SOME DATE 3</div>
  <div class="mt-4 feature-box">

### Foo 3
<span class="text-sm text-gray-400">TODO...</span>
  </div>
</div>
    
</div>
</div>

<div class="pop-up"
  v-click="[2, 3]"
  v-motion
    :initial="{ scale: 0.5 }"
    :enter="{ scale: 1 }"
    :leave="{ scale: 0.5 }">

<div>

<LocationBanner>

**Arak**

</LocationBanner>

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Arak_Heavy_Water4.JPG/1920px-Arak_Heavy_Water4.JPG" class="h-sm rounded-lg border-2 border-solid border-[--slidev-theme-primary]" />

</div>

</div>

<div class="pop-up ml-80 mt-34"
  v-click="[2, 3]"
  v-motion
    :initial="{ scale: 0, transition: { delay: 0 } }"
    :enter="{ scale: 1, transition: { delay: 1000 } }"
    :leave="{ scale: 0, transition: { delay: 0 } }">

<div>

<LocationBanner>

**Natanz**

</LocationBanner>

<img src="https://cdn.prod.www.spiegel.de/images/1ea2ca16-0001-0004-0000-000000166478_w960_r1.778_fpx28.91_fpy50.webp" class="h-sm rounded-lg border-2 border-solid border-[--slidev-theme-primary]" />

</div>

</div>

---
layout: end
---

<script setup>
import { vGlitch } from 'vue-powerglitch'

const glitch = {
  "timing": {
    "duration": 5000
  },
  "shake": {
    "velocity": 15,
    "amplitudeX": 0.3,
    "amplitudeY": 0.3,
  },
  "glitchTimeSpan": {
    "start": 0.5,
    "end": 0.7,
  }
}
</script>

<div
  v-motion
    :initial="{ y: 0, opacity: 0 }"
    :enter="{ y: -190, opacity: 1, transition: { delay: 4000, duration: 1000, opacity: { delay: 1000 } } }"
>
<div v-glitch="glitch">

# Danke für die Aufmerksamkeit

<PoweredBySlidev />

</div>
</div>

<div
  class="text-left"
  style="
    position: absolute;
    left: 3rem;
    top: 10rem;
  "
  v-motion
    :initial="{ x: 1000 }"
    :enter="{ x: 0, transition: { delay: 4500, duration: 1500 } }"
>

# Sources

- https://www.youtube.com/watch?v=Lc6qNCVHyFo
- https://www.csoonline.com/article/562691/stuxnet-explained-the-first-known-cyberweapon.html

</div>
