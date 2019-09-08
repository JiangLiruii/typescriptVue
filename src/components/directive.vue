<template>
  <div>
    <h1 v-log>Directive Simple</h1>
    <span v-logComplicated="complicateText">{{complicateText}}</span>
    <button @click="changeText">click me</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
@Component({
  directives: {
    // 简易版本, bind和update相同
    log(el, binding, vnode) {
      console.log(el.textContent);
    },
    // 复杂版本
    logComplicated: {
      // 在bind时触发
      bind(el, binding, vnode) {
        console.log(
          'this log from directive bind',
          el.textContent,        // Directive Complicate
          'binding Name:',
          binding.name,         // logComplicated
          'binding Value:',
          binding.value,        // lorry
          'vnodeTag',
          vnode.tag,            // h2
        );
      },
      // 组件更新时
      componentUpdated(el, binding, vnode) {
        console.log('Directive Component Changed from', binding.oldValue, 'to', binding.value);
      },
    },
  },
})
export default class Directive extends Vue {
  private complicateText = 'complicate'

  private changeText() {
    this.complicateText = 'Text changed';
  }
}
</script>
