<template>
  <div class="box">
    <div class="columns">
      <form class="column is-8" role="form" aria-label="Formulário de tarefa">
        <input 
        type="text"
        class="input"
        placeholder="Digite o nome da tarefa!"
        v-model="description"
        @input="charQuantity"
        autocapitalize="sentences"
        autocomplete="off"
        autofocus
        >
        <TimerButtonsComponent @onTimerFinished="stopTask" :value="description" class="show"/>
      </form>
      <div class="greeAlert">
        <p>A descrição deve conter 60 caracteres!</p>
        <p>Quantidade atual: {{ quantity }}.</p>
        <p>Restante: {{ 60 - quantity }}.</p>
      </div>
      <div class="redAlert">
        <p>Limite atingido!</p>
        <p>Quantidade atual: {{ quantity }}.</p>
        <p>Restante: {{ 60 - quantity }}.</p>
      </div>
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
  computed: {
    quantity(): number {
      return this.description.length;
    },
  },
  methods: {
    stopTask(timeInSeconds: number): void {
      this.$emit('onSaveTask', {
        description: this.description,
        durationInSeconds: timeInSeconds,
      });
      this.description = '';
    },
    closeModal(): void {
      this.$el.querySelector('.modal').style.display = 'none';
    },
    charQuantity(): void {
      if (this.quantity > 60) {
        this.$el.querySelector('.redAlert').style.display = 'flex';
        this.$el.querySelector('.greeAlert').style.display = 'none';
      } else {
        this.$el.querySelector('.redAlert').style.display = 'none';
        this.$el.querySelector('.greeAlert').style.display = 'flex';
      }
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
  margin: 20px;
}

form{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 90%;
  margin: 0 auto;
}

input {
  border: none;
  border-bottom: 1px solid #000000;
  border-radius: 0;
  box-shadow: none;
  outline: none;
  width: 90%;
  -webkit-rtl-ordering: logical;
}

input:focus {
  border-color: #000000;
  box-shadow: none;
}

input::placeholder {
  text-align: center;
}

.greeAlert{
  padding: 5px;
  background-color: #C8E6C9;
  border-radius: 8px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}


.redAlert{
  padding: 5px;
  background-color: #FFCDD2;
  border-radius: 8px;
  width: 100%;
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

.greeAlert p, .redAlert p{
  font-family: Arial, sans-serif;
  color: #000000;
  text-align: center;
  font-weight: bold;
  font-size: 12px;
}

</style>