<template>
  <div>
    <p>这是演示filter</p>
    <span>{{'hello' | addWorld}}</span>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
@Component({
  filters: {
    addWorld: (value: string) => `${value} world`,
  },
})
export default class FilterComponent extends Vue {
}
</script>
