<template>
  <div class="box">
    <div class="columns">
      <div class="column is-8" role="form" aria-label="Formulário de tarefa">
        <input type="text" class="input" placeholder="Digite o nome da tarefa!" v-model="description">
      </div>
      <TimerButtonsComponent @onTimerFinished="stopTask" :value="description"/>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TimerButtonsComponent from './TimerButtonsComponent.vue';

export default defineComponent({
  name: 'FormComponent',
  components: {
    TimerButtonsComponent,
  },
  emits: ['onSaveTask'],
  data() {
    return {
      description: '',
      elapsedTime: '',
    };
  },
  methods: {
    stopTask(timeInSeconds: number): void {
      this.$emit('onSaveTask', {
        description: this.description,
        durationInSeconds: timeInSeconds,
      });
      this.description = '';
    },
  },
});

</script>

<style scoped>

.columns{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

input {
  border: none;
  border-bottom: 1px solid #000000;
  border-radius: 0;
  box-shadow: none;
  outline: none;
}

input:focus {
  border-color: #000000;
  box-shadow: none;
}

input::placeholder {
  text-align: center;
}

</style>