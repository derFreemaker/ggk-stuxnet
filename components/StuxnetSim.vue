<template>
  <div class="stuxnet-sim-container">
    <div class="step-indicator">
      <div v-for="i in 5" :key="i" :class="['step', { active: currentStep === i, completed: currentStep > i }]">
        {{ i }}
      </div>
    </div>

    <div class="game-grid">
      <div class="main-panel">
        <div v-if="!showFinal">
          <div class="scenario-box">
            <span class="phase-tag">PHASE {{ currentStep }}</span>
            <div class="scenario-text" v-html="currentQ.scenario"></div>
          </div>
          
          <div class="decision-section">
            <h3 class="q-title">{{ currentQ.question }}</h3>
            <div class="options-list">
              <div 
                v-for="opt in shuffledOptions" 
                :key="opt.id"
                :class="['opt-card', { 
                  selected: selectedId === opt.id,
                  correct: submitted && opt.correct,
                  wrong: submitted && selectedId === opt.id && !opt.correct,
                  disabled: submitted
                }]"
                @click="handleSelect(opt.id)"
              >
                <div class="opt-header">
                  <span class="opt-title">{{ opt.title }}</span>
                  <span v-if="submitted && opt.correct" class="status-icon">✓</span>
                </div>
                <div class="opt-desc">{{ opt.desc }}</div>
              </div>
            </div>
          </div>

          <transition name="fade">
            <div v-if="submitted" :class="['feedback-box', isCorrect ? 'success' : 'warning']">
              {{ feedbackText }}
            </div>
          </transition>

          <div class="controls">
            <button v-if="!submitted" :disabled="!selectedId" @click="submit" class="btn-submit">Entscheidung treffen</button>
            <button v-if="submitted" @click="next" class="btn-next">Weiter →</button>
          </div>
        </div>

        <div v-else class="final-result" :class="missionStatus.class">
          <h2>{{ missionStatus.title }}</h2>
          <p class="res-text">{{ missionStatus.text }}</p>
          
          <div class="learning-points">
            <h4>Lessons Learned:</h4>
            <ul>
              <li><strong>Präzision:</strong> Spezialisierte Ziele minimieren Kollateralschäden.</li>
              <li><strong>Tarnung:</strong> Fake-Daten halten Operatoren im Dunkeln.</li>
              <li><strong>Risiko:</strong> Globale Verbreitung führt zur Entdeckung.</li>
            </ul>
          </div>

          <button @click="reset" class="btn-reset">🔄 Simulation Neustarten</button>
        </div>
      </div>

      <div class="side-panel">
        <h4 class="side-title">📊 MISSION STATUS</h4>
        <div v-for="(val, key) in stats" :key="key" class="stat-row">
          <div class="stat-label">
            <span>{{ keyLabels[key] }}</span>
            <span>{{ Math.round(val) }}%</span>
          </div>
          <div class="bar-bg">
            <div :class="['bar-fill', key]" :style="{ width: val + '%' }"></div>
          </div>
        </div>
        
        <div class="log-area">
          <div class="log-title">EVENT LOG</div>
          <div class="log-content">
            <div v-for="(log, i) in eventLogs" :key="i" class="log-entry">
              ▸ {{ log }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const questions = [
  {
    step: 1,
    scenario: "<strong>Infiltration</strong>: Die Atomanlage ist komplett vom Internet getrennt (Air-Gap).",
    question: "Wie bringst du den Virus in die Anlage?",
    options: [
      { id: "usb", title: "🔌 USB-Zulieferer", desc: "Infiziere Sticks eines Wartungstechnikers.", impact: { success: 15, detection: 5, budget: -20 }, correct: true, feedback: "Klassischer Stuxnet-Weg. Effektiv und unauffällig." },
      { id: "hack", title: "💻 Remote Hack", desc: "Versuche die Firewall zu durchbrechen.", impact: { success: -20, detection: 40, budget: 0 }, correct: false, feedback: "Fehler! Ohne Internetverbindung schlägt dieser Versuch fehl." },
      { id: "insider", title: "👤 Insider", desc: "Bestiche einen Mitarbeiter vor Ort.", impact: { success: 10, detection: 25, budget: -40 }, correct: false, feedback: "Riskant. Menschen sind unzuverlässig und teuer." }
    ]
  },
  {
    step: 2,
    scenario: "<strong>Zielsystem</strong>: Der Virus ist im Netzwerk. Er sucht die Zentrifugen-Steuerung.",
    question: "Wie soll sich der Virus verbreiten?",
    options: [
      { id: "specific", title: "🎯 Spezifisch", desc: "Suche nur nach Siemens S7-300 Steuerungen.", impact: { success: 20, detection: -10, budget: -10 }, correct: true, feedback: "Richtig. So bleibt der Virus auf normalen PCs unsichtbar." },
      { id: "broad", title: "🌐 Masseninfektion", desc: "Infiziere jeden verfügbaren Knoten.", impact: { success: 5, detection: 50, budget: 0 }, correct: false, feedback: "Viel zu auffällig. Die IT-Abteilung schlägt sofort Alarm." }
    ]
  },
  {
    step: 3,
    scenario: "<strong>Tarnung</strong>: Du hast die Kontrolle. Die Operatoren dürfen nichts merken.",
    question: "Welche Tarnung wählst du?",
    options: [
      { id: "rootkit", title: "👻 Rootkit", desc: "Zeige den Monitoren gefälschte Normalwerte.", impact: { success: 25, detection: -20, budget: -25 }, correct: true, feedback: "Genial. Die Techniker sehen 'alles okay', während die Hardware stirbt." },
      { id: "disable", title: "🔇 Alarm-Off", desc: "Deaktiviere die Warnsirenen.", impact: { success: 5, detection: 40, budget: -5 }, correct: false, feedback: "Verdächtig. Wenn Systeme schweigen, wird manuell geprüft." }
    ]
  },
  {
    step: 4,
    scenario: "<strong>Sabotage</strong>: Die Zentrifugen müssen physisch zerstört werden.",
    question: "Wähle die Angriffsmethode:",
    options: [
      { id: "speed", title: "⚙️ Frequenz-Manipulation", desc: "Ändere die Drehzahl extrem schnell.", impact: { success: 25, detection: 10, budget: 0 }, correct: true, feedback: "Effektiv. Das Material wird müde und bricht ohne Explosion." },
      { id: "explosion", title: "💥 Überlastung", desc: "Drehe bis zum Maximum auf.", impact: { success: 10, detection: 60, budget: 0 }, correct: false, feedback: "Zu laut. Eine Explosion führt zur sofortigen Untersuchung." }
    ]
  },
  {
    step: 5,
    scenario: "<strong>Exit</strong>: Der Schaden ist angerichtet. Was passiert mit dem Code?",
    question: "Wähle die Exit-Strategie:",
    options: [
      { id: "self", title: "💣 Kill-Switch", desc: "Virus löscht sich nach Datum X selbst.", impact: { success: 10, detection: -15, budget: -5 }, correct: true, feedback: "Klug. So erschwerst du die forensische Analyse enorm." },
      { id: "global", title: "🌍 Weltweite Ausbreitung", desc: "Lass den Virus ins Internet entkommen.", impact: { success: -20, detection: 80, budget: 0 }, correct: false, feedback: "Katastrophe. Genau das passierte bei Stuxnet und enttarnte alles." }
    ]
  }
]

// State
const stats = ref({ success: 40, detection: 20, budget: 100 })
const keyLabels = { success: 'Erfolg', detection: 'Risiko', budget: 'Budget' }
const currentIdx = ref(0)
const selectedId = ref(null)
const submitted = ref(false)
const showFinal = ref(false)
const eventLogs = ref(['Mission gestartet...'])
const shuffledOptions = ref([])

const currentQ = computed(() => questions[currentIdx.value])
const currentStep = computed(() => currentQ.value.step)
const isCorrect = computed(() => currentQ.value.options.find(o => o.id === selectedId.value)?.correct)
const feedbackText = computed(() => currentQ.value.options.find(o => o.id === selectedId.value)?.feedback)

const missionStatus = computed(() => {
  if (stats.value.detection > 75) return { title: "ENTDECKT!", class: "failed", text: "Die Gegenseite hat den Code isoliert. Mission gescheitert." }
  if (stats.value.success > 70) return { title: "MISSION ERFOLGREICH", class: "success", text: "Die Zentrifugen sind Schrott. Der Gegner ist um Jahre zurückgeworfen." }
  return { title: "TEILERFOLG", class: "neutral", text: "Schaden verursacht, aber der Virus wurde gefunden." }
})

// Logik
const shuffle = (array) => [...array].sort(() => Math.random() - 0.5)

const handleSelect = (id) => {
  if (!submitted.value) selectedId.value = id
}

const submit = () => {
  const opt = currentQ.value.options.find(o => o.id === selectedId.value)
  stats.value.success = Math.min(100, Math.max(0, stats.value.success + opt.impact.success))
  stats.value.detection = Math.min(100, Math.max(0, stats.value.detection + opt.impact.detection))
  stats.value.budget = Math.min(100, Math.max(0, stats.value.budget + opt.impact.budget))
  
  eventLogs.value.unshift(opt.correct ? "✓ Ziel erreicht" : "⚠ Komplikationen")
  submitted.value = true
}

const next = () => {
  if (currentIdx.value < questions.length - 1) {
    currentIdx.value++
    selectedId.value = null
    submitted.value = false
    shuffledOptions.value = shuffle(currentQ.value.options)
  } else {
    showFinal.value = true
  }
}

const reset = () => {
  currentIdx.value = 0
  stats.value = { success: 40, detection: 20, budget: 100 }
  showFinal.value = false
  submitted.value = false
  selectedId.value = null
  eventLogs.value = ['Mission neu gestartet...']
  shuffledOptions.value = shuffle(questions[0].options)
}

onMounted(() => {
  shuffledOptions.value = shuffle(questions[0].options)
})
</script>

<style scoped>
.stuxnet-sim-container {
  font-family: 'JetBrains Mono', monospace, sans-serif;
  color: #e0e0e0;
  max-width: 900px;
  margin: auto;
}

.game-grid {
  display: grid;
  grid-template-columns: 1.8fr 1fr;
  gap: 1.5rem;
}

.main-panel {
  background: rgba(20, 25, 35, 0.95);
  padding: 1.5rem;
  border-radius: 12px;
  border: 1px solid #00ff8844;
  min-height: 420px;
}

.scenario-box {
  background: rgba(0, 0, 0, 0.4);
  padding: 1rem;
  border-left: 4px solid #00ff88;
  margin-bottom: 1.5rem;
}

.phase-tag {
  font-size: 0.7rem;
  color: #00ff88;
  font-weight: bold;
}

.opt-card {
  background: rgba(255, 255, 255, 0.05);
  padding: 0.8rem;
  margin: 0.5rem 0;
  border-radius: 6px;
  cursor: pointer;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.2s;
}

.opt-card:hover:not(.disabled) {
  border-color: #00ff88;
  background: rgba(0, 255, 136, 0.05);
}

.opt-card.selected {
  border-color: #00ff88;
  background: rgba(0, 255, 136, 0.15);
}

.opt-card.correct { border-color: #00ff88; background: rgba(0, 255, 136, 0.2); }
.opt-card.wrong { border-color: #ff4444; background: rgba(255, 68, 68, 0.2); }

.opt-title { font-weight: bold; display: block; margin-bottom: 0.2rem; }
.opt-desc { font-size: 0.85rem; opacity: 0.8; }

.side-panel {
  background: rgba(15, 20, 30, 0.8);
  padding: 1.2rem;
  border-radius: 12px;
}

.stat-label {
  display: flex;
  justify-content: space-between;
  font-size: 0.8rem;
  margin-bottom: 0.3rem;
}

.bar-bg {
  background: #222;
  height: 8px;
  border-radius: 4px;
  margin-bottom: 1rem;
  overflow: hidden;
}

.bar-fill { height: 100%; transition: width 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
.bar-fill.success { background: #00ff88; box-shadow: 0 0 10px #00ff8888; }
.bar-fill.detection { background: #ff4444; }
.bar-fill.budget { background: #44aaff; }

.feedback-box {
  padding: 0.8rem;
  border-radius: 6px;
  margin-top: 1rem;
  font-size: 0.9rem;
}
.feedback-box.success { background: rgba(0, 255, 136, 0.1); color: #00ff88; border: 1px solid #00ff88; }
.feedback-box.warning { background: rgba(255, 200, 0, 0.1); color: #ffcc00; border: 1px solid #ffcc00; }

.btn-submit, .btn-next, .btn-reset {
  width: 100%;
  padding: 0.8rem;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  border: none;
  margin-top: 1rem;
}

.btn-submit { background: #00ff88; color: #002211; }
.btn-submit:disabled { opacity: 0.3; cursor: not-allowed; }
.btn-next { background: #44aaff; color: white; }
.btn-reset { background: #333; color: white; border: 1px solid #666; }

.step-indicator { display: flex; justify-content: center; gap: 0.8rem; margin-bottom: 1.5rem; }
.step {
  width: 32px; height: 32px; border-radius: 50%; border: 2px solid #444;
  display: flex; align-items: center; justify-content: center; font-size: 0.8rem;
}
.step.active { border-color: #00ff88; color: #00ff88; box-shadow: 0 0 10px #00ff8844; }
.step.completed { background: #00ff88; border-color: #00ff88; color: #002211; }

.log-area { margin-top: 2rem; }
.log-title { font-size: 0.7rem; opacity: 0.5; border-bottom: 1px solid #333; margin-bottom: 0.5rem; }
.log-entry { font-size: 0.75rem; color: #888; margin-bottom: 0.2rem; }

.final-result h2 { color: #00ff88; margin-bottom: 1rem; }
.final-result.failed h2 { color: #ff4444; }

.fade-enter-active, .fade-leave-active { transition: opacity 0.3s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
</style>
