<!--
  checkbox 组件
  @param {Array<Object>} data 传入checkbox组件数据,用于渲染
      ex: [{
          value: 0,
          label: 'value0'
        }, {
          value: 1,
          label: 'value1'
        }, {
          value: 2,
          label: 'value2',
          isDisabled: true
        }]

  @param {Array} resultList 传入结果数组,用于接收设置和接收结果
  @param {value} value 如果没有传入resultList就使用value接收结果,如果有传入resultList相当于resultList[0]
  @param {Boolean} isVertical checkbox横向(false)排列还是纵向(true),默认为横向
  @param {Object} appendClass 自定义class
  @param {Object} appendStyle 自定义Style对象
-->
<template>
  <div v-for="it in data" track-by="$index" :style="appendStyle" :class="[appendClass]">
    <label class="tbd-label" :class="{'tbd-label-checked': (resultList && (it.value === resultList[$index]) || value === true), 'tbd-label-disabled': it.isDisabled}" @click="toggleSwitch($index, it.value)">
      <span class="tbd-checkbox"></span>
      <span class="tbd-label-text">
          {{{it.label || it.value}}}
      </span>
    </label>
  </div>
</template>

<script>
  import {componentBaseParamConfig} from '../base-config';

  export default {
    props: Object.assign({}, componentBaseParamConfig, {
      data: {
        type: Array,
        default: function() {
          return [{
            value: false,
            label: ' '
          }];
        }
      },
      resultList: {
        type: Array
      },
      isVertical: {
        type: Boolean,
        default: false
      },
      value: {}
    }),

    compiled() {
      this.appendStyle = Object.assign({}, this.appendStyle, {
        display: this.isVertical ? 'block' : 'inline-block'
      })
    },

    data () {
      return {
        isDisabled: ''
      }
    },

    methods: {
      toggleSwitch(index, value) {
        if(this.data[index].isDisabled) return;

        if(this.resultList) {
          this.resultList.$set(index, (this.resultList[index] === undefined || this.resultList[index] === '') ? value : '');
          this.value = resultList[0];
        } else {
          this.value = !this.value;
        }
      }
    }
  }
</script>

<style scoped>
  @import "style.css";
</style>