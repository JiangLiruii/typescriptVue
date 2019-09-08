<template>
  <div>
      <button @click="onClick">EmitButton</button>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
import { Component, Emit } from 'vue-property-decorator';
@Component
export default class EmitComponent extends Vue {
@Emit('childComponentClick')
  private onClick(e:any) {
    console.log(this, e);
    return 'child data';
  }
}
</script>
