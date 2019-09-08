<template>
  <div>
      <input type="checkbox" name="isDeep" v-model="isDeep" id="">
      <span>switch deep mode</span>
      <input type="text" v-model="person.name.firstName">
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
import { Component, Watch } from 'vue-property-decorator';

interface Iperson{
    name: { firstName: String; lastName: String };
    age: Number;
}
@Component
export default class WatchComponent extends Vue {
    private person:Iperson = { name: { firstName: 'JIANG', lastName: 'Lorry' }, age: 18 }

    private isDeep = false

    // 监听属性以及是否深度监听
    @Watch('person', {
      deep: true,
    })
    private personChanged(newer: Iperson, older: Iperson) {
      console.log('Is newer always equal to watched property value: ', this.person === newer);
      console.log('Watch person changed from ',
        newer.name.firstName, 'to', older.name.firstName);
    }
}
</script>
