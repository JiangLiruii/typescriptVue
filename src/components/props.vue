<template>
    <div>
        <h1>this is parent name Prop: {{name}}</h1>
        <input type="text" v-model="parentAge" >
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop, PropSync } from 'vue-property-decorator';

@Component
export default class PropComponent extends Vue {
    @Prop({
      // 配置类型
      type: String,
      // 配置是否必须
      required: true,
      // name必须包含'lorry', 可在parent的name data中进行修改, 不符合的将会告警
      validator: (value: string) => value.includes('lorry'),
    })
    private name!:string;

    // 可以实现父子组件的数据共享, 不能为同一标识符
    @PropSync('age')
    private parentAge!:string;
}
</script>
