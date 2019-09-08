<template>
  <div id="app">
    <h1>I'm parent</h1>
    <h2>Parent name data: <input type="text" v-model="name"></h2>
    <h2>{{`Parent age data: ${age}`}}</h2>
    <img alt="Vue logo" src="./assets/logo.png">
    <FilterComponent/>
    <hr>
    <DirectiveComponent/>
    <hr>
    <PropComponent :name="name" :age.sync="age" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import FilterComponent from './components/filter.vue';
import DirectiveComponent from './components/directive.vue';
import PropComponent from './components/props.vue';

@Component({
  components: {
    FilterComponent,
    DirectiveComponent,
    PropComponent,
  },
})
export default class App extends Vue {
  private age = 18

  private name = 'lorry'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
