<template>
  <div>
    <div class="box has-text-weight-bold alerta">
      <div class="columns">
        <div class="column is-12">
          <span>Sem Registro!</span>
        </div>
      </div>
    </div>

  </div>
</template>



<script lang="ts">

import { defineComponent } from 'vue';
export default defineComponent({
  name: 'NoTaskComponent'
});

</script>

<style scoped>

.box{
  margin: 1rem;
  text-align: center;
}

.alerta {
  background-color: #F3E5F5;
  border-radius: 8px;
  width: 60%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

.alerta span {
  font-family: Arial, sans-serif;
  color: #000000;
  text-align: center;
}

</style>