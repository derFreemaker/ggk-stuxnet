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
  <div class="desc">
  
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
  <div class="desc">

Entwicklungszeit von **2-3 Jahren** mit einem Team von **10 Personen**
  </div> 
</div>

<div class="feature-box items-center"
  v-click="5"
  v-motion
    :initial="{ x: -100 }"
    :enter="{ x: 0 }">
  <Factory class="mb-4" size="36"/>
  <div class="desc">

erste bekannter digitaler Angriff auf **industrielle Infrastruktur**
  </div>
</div>

<div class="feature-box items-center"
  v-click="6"
  v-motion
    :initial="{ y: 100 }"
    :enter="{ y: 0 }">
  <BrickWallFire class="mb-4" size="36" />
  <div class="desc">

verwendete **gestohlene Zertifikate**,<br> und **<span v-mark.underline.orange="7">4 Zero-Days</span>**
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
<div class="desc">
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
  <div class="desc">

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
  <div class="desc">

Einen "Zero-Day" zu kennen wird als **glücklich** bezeichnet.
  </div>
</div>

</div>

---
transition: slide-left
---

<script setup>
import { RouteOff, Shield } from 'lucide-vue-next';
</script>

# Wofür wurde STUXnet entwickelt?

<div class="mt-12 h-full timeline-window" v-click>
<div class="timeline"
  v-motion
    :initial="{ y: '0rem' }"
    :click-5="{ y: '-25.5rem' }"
    :click-11="{ y: '-51rem' }"
    :click-14="{ y: '-38.5rem' }"
    :click-15="{ y: '-51rem' }">

<div class="timeline-node" v-click="[1, 5]">
  <div class="mb-4">August 2002</div>
  <div class="feature-box">

### Aufdeckung von Nuklearanlagen
<div class="desc">

Eine iranische Wiederstandsgruppe deckt zwei unbekannte iranische Nuklearanlagen auf<span v-click="3">, Arak und Natanz.</span>
</div>
  </div>
  <br>

  <div class="feature-box" v-click="[4, 5]">
  
### Iran baut Atomwaffen?
<div class="desc">

Im Westen wächst die Vermutung das Iran Atomwaffen bauen will, vorallem da der Iran 1968 das Atomabkommen unterzeichnet haben. Wodurch Iran der **IAEA** von denn Analagen hätte erzählen müssen. Eine Untersuchung von der **IAEA** nachträglich offenbart das Natanz hochangereichertes Uran herstellt.
</div>
  </div>
</div>

<div class="timeline-node" v-click="[5, 11]">
  <div class="mb-4">2006</div>
  <div class="feature-box">

### Operation: Olympic Games
<div class="desc">

Die USA und Israel starten mit dem Bau einer Cyberwaffe um das iranische Atomprogramm gezielt zu sabotieren.
</div>
  </div>
</div>

<div class="timeline-node" v-click="[6, 15]">
  <div class="mb-4">2007</div>
  <div class="feature-box">

### Probleme bei Olympic Games
<div class="desc">

Trotz der Fortschritte von Olympic Games, stellt sich das Problem wie sie den Wurm in die Anlage Natanz bekommen. Da sie <span v-mark.underline.orange="7">**"air-gapped"**</span> ist aus Sicherheitsgründen.
</div>
  </div>
</div>

<div class="timeline-node" v-click="11">
  <div class="mb-4">Juni 2009</div>
  <div class="feature-box">

### Olympic Games startet
<div class="desc">

STUXnet gelangt in die Analage Natanz, über kompromittierte Zuliefer oder Wartungstechniker.
</div>
  </div>
</div>

<div class="timeline-node" v-click="12">
  <div class="mb-4">Juni 2010</div>
  <div class="feature-box">

### Olympic Games wurde gefunden
<div class="desc">

STUXnet wird entdeckt, <span v-mark.underline.orange="13">aber außerhalb von Natanz</span>, bei einer IT-Sicherheitsfirma.<br> Der Name "STUXnet" oder "Stuxnet" setzt sich zusammen aus gefunden Wörtern im Code.
</div>
  </div>
</div>

</div>
</div>

<!--  -->
<div class="pop-up p-4 ml-80 mt-34"
  v-click="[2, 3]"
  v-motion
    :initial="{ scale: 0 }"
    :enter="{ scale: 1 }"
    :leave="{ scale: 0 }">

<div>

<LocationBanner>

**Natanz**

</LocationBanner>

<img src="https://cdn.prod.www.spiegel.de/images/1ea2ca16-0001-0004-0000-000000166478_w960_r1.778_fpx28.91_fpy50.webp" class="h-sm rounded-lg border-2 border-solid border-[--slidev-theme-primary]" />

</div>

</div>
<!--  -->

<!--  -->
<div class="pop-up p-4"
  v-click="[2, 3]"
  v-motion
    :initial="{ scale: 0, transition: { delay: 0 } }"
    :enter="{ scale: 1, transition: { delay: 400 } }"
    :leave="{ scale: 0, transition: { delay: 0 } }">

<div>

<LocationBanner>

**Arak**

</LocationBanner>

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Arak_Heavy_Water4.JPG/1920px-Arak_Heavy_Water4.JPG" class="h-sm rounded-lg border-2 border-solid border-[--slidev-theme-primary]" />

</div>

</div>
<!--  -->

<!--  -->
<div class="pop-up p-2 size-full"
  v-click="[8, 11]"
  v-motion
    :initial="{ scale: 0 }"
    :enter="{ scale: 1 }"
    :leave="{ scale: 0 }">

<div class="border border-[--slidev-theme-primary] rounded-xl bg-[#121212] p-4 size-full">

<div class="mt-8 text-center">

## Was ist eine "Air-Gap"?
<div class="desc">
(Netzwerke)
</div>

</div>

<div class="grid grid-cols-2 gap-8 mt-16 px-8 text-center">
  
<div class="feature-box items-center"
  v-click="9"
  v-motion
    :initial="{ x: -100, y: -200, scale: 1.2 }"
    :enter="{ x: 50, y: 0 }"
      :click-10="{ x: 0, scale: 1 }">
  <RouteOff class="mb-4 text-color-[--slidev-theme-primary]" size="48" />
  <div class="font-bold text-xl mb-2">keine Verbindung</div>
  <div class="desc">

Es besteht **keine physikalische Verbindung** nach Außen, weder Drahtlos noch per Kabel.
  </div>
</div>

<div class="feature-box items-center"
  v-click="10"
  v-motion
    :initial="{ y: 200 }"
    :enter="{ y: 0 }">
  <Shield class="mb-4 text-color-[--slidev-theme-primary]" size="48" />
  <div class="font-bold text-xl mb-2">Sicherheit</div>
  <div class="desc">

Es ist eine **unüberwindbare Hürde** für Angreiffer aus der ferne, und **schließt mögliche Sicherheitslücken** welche in Software existieren können.
  </div>
</div>

</div>

</div>

</div>
<!--  -->

---
transition: slide-left
---

<script setup>
import { Worm, HatGlasses, RotateCw, Joystick } from 'lucide-vue-next';
</script>

# Was macht STUXnet?

<div class="grid grid-cols-2 gap-8 p-8 relative">
  
  <div v-click class="feature-box">
    <div class="step-num">1</div>
<div class="flex flex-row gap-4">
<Worm class="text-color-[--slidev-theme-primary]" size="36" />

### Infizierung
</div>
<div class="desc mt-4">

STUXnet gelangt in ein System und sucht nach einer bestimmte Software **"Siemens-Step 7"**.
</div>
  </div>

  <div v-click class="feature-box">
    <div class="step-num">2</div>
<div class="flex flex-row gap-4">
<HatGlasses class="text-color-[--slidev-theme-primary]" size="36" />

### Beobachtung
</div>
<div class="desc mt-4">
STUXnet zeichnet über längere Zeit den normalen Betrieb auf.
</div>
  </div>
  
  <div v-click class="feature-box">
    <div class="step-num">3</div>
<div class="flex flex-row gap-4">
<RotateCw class="text-color-[--slidev-theme-primary]" size="36" />

### Tarnung
</div>

<div class="desc mt-4">
Das aufgezeichnete Normalverhalten von Messwerten wird an den Kontrollraum weitergegeben, statt den eingentlichen Daten. 
</div>
  </div>

  <div v-click class="feature-box">
    <div class="step-num">4</div>
<div class="flex flex-row gap-4">
<Joystick class="text-color-[--slidev-theme-primary]" size="36" />

### Manipulation
</div>

<div class="desc mt-4">

STUXnet steuert die **Frequenzumricherter** an, welche die **Geschwindigkeit der Zentrifugen** steuern.
</div>
  </div>
</div>

<style>
.feature-box {
  @apply relative items-center;
}

.feature-box .step-num {
  @apply absolute -top-3 -left-3 w-8 h-8 bg-[--slidev-theme-primary] text-white rounded-full 
         flex items-center justify-center text-base font-bold shadow-2xl;
}
</style>

<!--
Normal: 807-1207Hz

Manipulation:
- erhöht auf 1410Hz
- reduziert auf 2Hz
- erhöht auf 1064Hz
- repeat
-->

---
transition: slide-left
layout: image-left
image: https://cdn.prod.www.spiegel.de/images/1ea2ca16-0001-0004-0000-000000166478_w960_r1.778_fpx28.91_fpy50.webp
---

<script setup>
import { Check } from 'lucide-vue-next';
</script>

# Auswirkungen in Natanz

<div
  v-click="1"
  v-motion
    :initial="{ y: 100 }"
    :enter="{ y: 0 }">

> **ca. 1000 Zentrifugen** wurden **zerstört**
> 
> von ca. 9000 Zentrifugen
</div>
<br>

<div
  v-click="2"
  v-motion
    :initial="{ x: -100 }"
    :enter="{ x: 0 }">

> iranisches Atomprogramm wurde um **1-2 Jahre** verzögert
</div>
<br>

<div class="feature-box"
  v-click="3"
  v-motion
    :initial="{ x: 100, y: 100 }"
    :enter="{ x: 0, y: 0 }">

<div class="flex flex-row gap-4">
<Check class="text-color-[--slidev-theme-primary]" size="36" />

## Erfolg?
</div>

<div class="desc mt-4"
  v-click="4">

Die Anlage wurde erfolgreich **sabortiert**, auch wenn nicht für so lange wie vielleicht geplant.
Es war nicht die Idee sie **ganz zu zerstören**, sondern nur zu verlangsamen.
</div>
</div>

---
transition: slide-left
---

# War Deutschland beteiligt?
<br>

<div class="flex flex-col gap-8">

<div class="feature-box flex flex-row p-0 overflow-hidden"
  v-click="1"
  v-motion
    :initial="{ x: -100, y: '100%', scale: 1.05 }"
    :enter="{ x: 0, y: '50%' }"
    :click-2="{ y: '0%', scale: 1 }">

<img src="https://www.designtagebuch.de/wp-content/uploads/mediathek//2024/03/bundesnachrichtendienst-bnd-logo.jpg" class="w-30%"/>

<div class="size-full p-6">

## Operation "Olympic Games"
<div class="desc mt-4">

**Der Bundesnachrichtendienst (BND)** soll **involviert** gewesen sein, jedoch wie alle anderen **nicht bestätigt**.
</div>
</div>

</div>

<div class="feature-box flex flex-row p-0 overflow-hidden"
  v-click="2"
  v-motion
    :initial="{ y: 100 }"
    :enter="{ y: 0 }">

<img src="https://www.gspeakers.com/wp-content/uploads/2018/03/langner-260x330.jpg" class="w-30%"/>

<div class="size-full p-6">

## Forscher
<div class="desc mt-4">

**Ralph Langner** (links) und **Frank Rieger** (rechts) sind zwei der bekannten ersten deutschen Forscher. **Ralph Langer** wird auch als Experte für STUXnet interviewt.
</div>
</div>

<img src="https://cre.fm/files/2021/03/frank-rieger.jpg" class="w-35%"/>

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

# Sources:

<div class="text-xs">

- https://www.youtube.com/watch?v=Lc6qNCVHyFo
- https://www.csoonline.com/article/562691/stuxnet-explained-the-first-known-cyberweapon.html
- https://2001-2009.state.gov/r/pa/prs/ps/2003/20439.htm
- https://edition.cnn.com/2002/WORLD/meast/12/13/iran.nuclear/
- https://www.nytimes.com/2012/06/01/world/middleeast/obama-ordered-wave-of-cyberattacks-against-iran.html?_r=2&smid=tw-nytimes&seid=auto
- https://www.spiegel.de/politik/ausland/atomstreit-iran-brueskiert-den-westen-mit-neuen-uran-plaenen-a-664126.html
- https://www.researchgate.net/publication/267156195_Stuxnet_A_new_Cyberwar_weapon_Analysis_from_a_technical_point_of_view
</div>
</div>
