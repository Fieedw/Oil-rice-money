<template>
    <div>
        <ul class="types">
            <li :class="value==='-'&& 'selected'" @click="selectType('-')">支出</li>
            <li :class="value === '+'&& 'selected'" @click="selectType('+')">收入</li>
        </ul>
    </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';

  @Component
  export default class Types extends Vue {
  @Prop() readonly  value!: string;
// @Prop(Number) xxx: number | undefined;
// //Prop 告诉 Vue ，xxx不是data是 prop
// //Number 告诉 Vue, xxx运行时是个Number
// //xxx 属性名
// //number | undefined 告诉TS xxx的编译时类型
    selectType(type: string) {
      if (type !== '-' && type !== '+') {
        throw new Error('type is unknown');
      }
      this.$emit('update:value',type)
    }
  }
  //   @Watch('type')
  //   onTypeChanged(value: string){
  //     this.$emit('update:value',value)
  //   }
  // }
  // export default {
  //   name: 'Types',
  //   data() {
  //     return {
  //       type: '-'//-表示支出，+表示收入
  //     };
  //   },
  //   methods: {
  //     selectType(type) {
  //       if (type !== '-' && type !== '+') {
  //         throw new Error('type is unknown');
  //       }
  //       this.type = type;
  //     }
  //   }
  // };
</script>

<style lang="scss" scoped>
    .types {
        background: #c4c4c4;
        display: flex;
        text-align: center;
        font-size: 24px;

        > li {
            width: 50%;
            height: 64px;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;

            &.selected::after {
                content: '';
                position: absolute;
                bottom: 0;
                left: 0;
                width: 100%;
                height: 4px;
                background: #333;
            }
        }
    }
</style>