<template>
  <div class="painel">
    <h1>Temporizador de Tarefas</h1>
    <img src="../assets/logo.png" alt="Logo">
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'SideBarComponent',
});

</script>

<style scoped>

  .painel{
    background-color: #463994;
    padding: 1rem;
    width: 100%;
    height: 100vh;
    border: 10px solid #ffffff;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

  }

  h1{
    font-size: 1.5rem;
    font-weight: bold;
    color: #ffffff;
    text-align: center;
  }


  img{
    width: 200px;
    transform: rotate(6.8deg);
  }

  @media only screen and (max-width: 768px) {
    .painel{
      padding: 2.5rem;
      height: auto;
    }
  }

</style>