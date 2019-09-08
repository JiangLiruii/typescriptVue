<template>
  <div id="app">
    <div id="parent">
      <h1>I'm parent</h1>
      <h2>
        Parent name data:
        <input type="text" v-model="name" />
      </h2>
      <h2>{{`Parent age data: ${age}`}}</h2>
      <select name="showComponent" id="showComponent" v-model="showComponent">
        <option value="Filter">Filter</option>
        <option value="Emit">Emit</option>
      </select>
    </div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <component :is="CurrentComponent" v-bind="allProps"/>
    <!-- 无法通过传递所有props传递.sync v-on的数据, 参考 https://github.com/vuejs/vue/issues/4962#issuecomment-466930107 -->
    <PropComponent :name="name" :age.sync="age" />
    <EmitComponent v-on:childComponentClick="childButtonCLick" />
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator';
import FilterComponent from './components/filter.vue';
import DirectiveComponent from './components/directive.vue';
import PropComponent from './components/props.vue';
import EmitComponent from './components/emit.vue';

@Component({
  components: {
    FilterComponent,
    DirectiveComponent,
    PropComponent,
    EmitComponent,
  },
})
export default class App extends Vue {
  private age = 18;

  private CurrentComponent = FilterComponent;

  private name = 'lorry';

  private showComponent = 'Filter'

  private allProps = {
    name: 'lorry',
    showComponent: 'Filter',
    age: 18,
  }

  @Watch('showComponent')
  private ComponentChange(newValue: String) {
    console.log(newValue);
    switch (newValue) {
      case 'Filter':
        this.CurrentComponent = FilterComponent;
        break;
      default:
        break;
    }
  }

  private childButtonCLick(data:string, event:MouseEvent) {
    this.name = data;
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#parent {
  border: grey dotted 1px;
  padding: 10px;
}
</style>
