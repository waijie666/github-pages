<template>
  <div class="about">
    <h1>This website is just me learning about Vue</h1>
    <div>Environment variables</div>
    <div class="grid-container-parent">
      <div class="grid-container-child">
        <div>Key</div><div>Value</div>
      </div>
      <template v-for="(value, key) in env" :key="key">
        <div class="grid-container-child">
          <div>{{key}}</div><div>{{value}}</div>
        </div>
      </template>
    </div>
  </div>
</template>

<style scoped>
  .grid-container-parent {
    display: grid;
    grid-auto-flow: row;
  }
  .grid-container-child {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: minmax(200px, 1fr) minmax(200px, 1fr);
    margin: auto;
  }
</style>

<script>
export default {
    name: 'About',
    components: {
    },
    data()  {
        return  {
            env: process.env
        }
    }
}
</script>
