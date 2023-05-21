<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <SideBarComponent />
    </div>
    <div class="column is-three-quarter">
      <FormComponent @onSaveTask="addTask"/>
      <div class="list">
        <NoTaskComponent v-if="emptyList" />
        <TasksComponent v-for="(task, index) in tasks" :key="index" :task="task" />
      </div>
    </div>

  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SideBarComponent from './components/SideBarComponent.vue';
import FormComponent from './components/FormComponent.vue';
import TasksComponent from './components/TasksComponent.vue';
import ITask from './interfaces/ITask';
import NoTaskComponent from './components/NoTaskComponent.vue';

export default defineComponent({
  name: 'App',
  components: {
    SideBarComponent,
    FormComponent,
    TasksComponent,
    NoTaskComponent,
  },
  data() {
    return {
      tasks: [] as ITask[],
    }
  },
  computed: {
    emptyList(): boolean {
      return this.tasks.length === 0;
    },
  },
  methods: {
    addTask(task: ITask): void {
      this.tasks.push(task);
    },
  },
});
</script>

<style>

.list{
  padding: 1.25rem;
}


</style>
