<template>
  <div class="column">
    <CronometroComponent :timeInSeconds="timeInSeconds" />
    <div class="is-flex is-align-items-center is-justify-content-space-between">
      <button class="button play-btn" :disabled="isbtnStartActive || errorMsg" @click="startTask">
        <span class="icon">
          <i class="fas fa-play"></i>
        </span>
        <span>Iniciar</span>
      </button>
      <button class="button pause-btn" :disabled="isbtnStopActive" @click="pauseTask">
        <span class="icon">
          <i class="fas fa-pause"></i>
        </span>
        <span>Pausar</span>
      </button>
      <button class="button stop-btn" :disabled="isbtnStopActive || errorMsg" @click="stopTask">
        <span class="icon">
          <i class="fas fa-stop"></i>
        </span>
        <span>Parar</span>
      </button>
    </div>
    <p v-if="showAlert" class="alert">Informe uma tarefa com no mínimo 5 caracteres para iniciar!</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroComponent from './StopWatchComponent.vue';

export default defineComponent({
  name: 'TimerButtonsComponent',
  emits: ['onTimerFinished', 'stopTask'],
  components: {
    CronometroComponent,
  },
  data() {
    return {
      timeInSeconds: 0,
      isbtnStartActive: false,
      isbtnStopActive: true,
      stopwatch: 0,
      showAlert: false,
      errorMsg: false,
    };
  },
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  computed: {
    elapsedTime(): string {
      return new Date(this.timeInSeconds * 1000).toISOString().substr(11, 8);
    },
    isValid(): boolean {
      //check that the value is not empty and has at least 5 characters
      return this.value.trim().length >= 5;
    },
  },
  methods: {    
    startTask() {
      if (!this.isValid) {
        this.showAlert = true;
        this.errorMsg = true;
        setTimeout(() => {
          this.showAlert = false;
          this.errorMsg = false;
        }, 3000);
        return;
      }

      this.showAlert = false;

      if (!this.isbtnStartActive) {
        this.isbtnStartActive = true;
        this.isbtnStopActive = false;
        this.stopwatch = setInterval(() => {
          this.timeInSeconds++;
        }, 1000);
      }
    },
    pauseTask() {
      if (!this.isbtnStopActive) {
        this.isbtnStartActive = false;
        this.isbtnStopActive = true;
        clearInterval(this.stopwatch);
      }
    },
    stopTask() {
      if (!this.isValid) {
        this.showAlert = true;
        this.errorMsg = true;
        setTimeout(() => {
          this.showAlert = false;
          this.errorMsg = false;
        }, 3000);
        return;
      }

      if (!this.isbtnStopActive) {
        this.isbtnStartActive = false;
        this.isbtnStopActive = true;
        clearInterval(this.stopwatch);
        this.$emit('onTimerFinished', this.timeInSeconds);
        this.timeInSeconds = 0;
      }
    },
  }
});

</script>

<style scoped>

.column{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.play-btn {
  background-color: #389265;
  border: none;
  color: #ffffff;
  margin: 5px;
}

.play-btn:hover {
  background-color: #2e7d5a;
}

.play-btn:disabled {
  background-color: #389265;
  opacity: 0.5;
}

.pause-btn{
  background-color: #f7b731;
  border: none;
  color: #ffffff;
  margin: 5px;
}

.pause-btn:hover {
  background-color: #d9a126;
}

.pause-btn:disabled {
  background-color: #f7b731;
  opacity: 0.5;
}

.stop-btn {
  background-color: #ec002f;
  border: none;
  color: #ffffff;
  margin: 5px;
}

.stop-btn:hover {
  background-color: #c9002a;
}

.stop-btn:disabled {
  background-color: #ec002f;
  opacity: 0.5;
}

.play-btn, .pause-btn, .stop-btn {
  width: 120px;
  height: 40px;
  border-radius: 5px;
  font-weight: bold;
}

.alert{
  color: #ec002f;
  font-weight: bold;
  padding: 10px;
  margin: 10px;
}



</style>