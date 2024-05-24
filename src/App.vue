<template>
  <div id="app">
    <ParentComponent>
      <template v-slot>
        <p>Sloot</p>
      </template>
    </ParentComponent>
  </div>
</template>

<script>
import ParentComponent from './components/ParentComponent.vue';

export default {
  name: 'App',
  components: {
    ParentComponent
  }
};
</script>

<style>
#app {
  font-family: 'Arial', sans-serif;
  background-color: #ffffff;
  color: #333333;
  padding: 20px;
  text-align: center;
}
</style>
