<!--
  select 下拉列表
  @param {Object} data 传入组件数据,用于渲染
    ex:
        {
          optsList: [{
            value: 0,
            label: 'value0'
          }, {
            value: 1,
            label: 'value1'
            // 特性渲染函数
            render: function() {
                return <a>111</a>
            }
          }, {
            value: 2,
            label: 'value2',
            isDisabled: true
          }]
        }
  @param {String | Number} value 绑定外部数据对象的结果
  @param {Boolean} isDisabled 当前下拉列表是否可选
  @param {Boolean} isOpened 下拉列表是否显示
  @param {Function} onSelect 选择事件
  @param {Object} appendClass 自定义class
  @param {Object} appendStyle 自定义Style对象
-->
<template>
    <v-dropdown :data="data"
                :append-style="appendStyle"
                :append-class="appendClass"
                :value.sync="value"
                :is-disabled="isDisabled"
                :on-select="onSelected"
                :is-opened="isOpened">
        <span class="tbd-select-selection tbd-select-selection-single">
        <span class="tbd-select-selection-rendered">{{currentSelected}}</span>
        <span class="tbd-select-arrow" @click.stop="toggle"></span>
        </span>
    </v-dropdown>
</template>

<script>
import {componentBaseParamConfig} from '../base-config';
import vDropdown from '../dropdown';

export default {
    props: Object.assign({}, componentBaseParamConfig, {
        isDisabled: {
            type: Boolean,
            default: false
        },
        data: {
            type: Object,
            default: function() {
                return {
                    optsList: []
                }
            }
        },
        value: {
        },
        onSelect: {
            type: Function
        },
        isOpened: {
            type: Boolean,
            default: false
        }
    }),

    data () {
        return {}
    },

    computed: {
        currentSelected() {
            const _this = this;
            let res = _this.data.optsList.find(function(it) {
                return it.value == _this.value;
            });
            return res && (res.label || res.value) || '请选择';
        }
    },

    methods: {
        onSelected(index, item) {
            let opts = this.data.optsList;

            if(opts.isDisabled) return;

            this.currentSelected = opts[index].label || this.value;
            this.onSelect && this.onSelect(index, item.value);
        },

        toggle() {
            this.isOpened = !this.isOpened;
        }
    },

    components: {
        vDropdown
    }
}
</script>

<style scoped>
    @import "style.css";
</style>