<template>
  <div>
    <div class="box has-text-weight-bold">
      <div class="columns">
        <div class="column is-10">
          <p>Descrição:</p>
          <p class="black">{{ task.description || 'N/A'}}</p>
        </div>
        <div class="column is-2">
          <p>Duração:</p>
          <StopWatchComponent :timeInSeconds="task.durationInSeconds" />
        </div>
      </div>
    </div>

  </div>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue';
import StopWatchComponent from './StopWatchComponent.vue';
import ITask from '../interfaces/ITask';

export default defineComponent({
  name: 'TasksComponent',
  components: {
    StopWatchComponent,
}, props: {
  task: {
    type: Object as PropType<ITask>,
      required: true,
  }
}
});

</script>

<style scoped>

.box{
  background-color:  #c5c5c5;;
  margin: 1rem;
  text-align: center;
}

p{
  font-size: 1rem;
  font-weight: bold;
  color: #6A1B9A;
}

.black{
  color: #000000;
}

h1{
  font-size: 1rem;
  font-weight: bold;
  color: #363636;
}


</style>
