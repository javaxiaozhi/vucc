<!--
  switch 组件
  @param {Boolean} value 开关是否打开
  @param {String} [size=normal|large|small] 开关的大小
  @param {Object} appendClass 自定义class
  @param {Object} appendStyle 自定义Style对象
-->
<template>
  <div :style="appendStyle" :class="['tbd-switch', appendClass, sizeClass, value ? '' : 'tbd-switch-off']" @click="toggleSwitch"><i></i></div>
</template>

<script>
  import {componentBaseParamConfig} from '../base-config';

  export default {
    props: Object.assign({}, componentBaseParamConfig, {
      size: {
        type: String,
        default: 'normal'
      },
      value: {
        type: Boolean,
        default: false
      }
    }),

  data () {
    return {};
  },

  computed: {
    sizeClass() {
      const sizeMap = {
        'normal': '',
        'small': 'tbd-switch-sm'
      };

      return sizeMap[this.size]
    }
  },

  methods: {
    toggleSwitch() {
      this.value = !this.value;
    }
  }

  }
</script>

<style scoped>
  @import "style.css";
</style>