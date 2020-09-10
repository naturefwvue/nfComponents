/**勾选框，返回true和false */
<template>
  <!--单选组 radio_g_s  label radio_g_t-->
  <span>
    <label role="checkbox" v-for="item in meta.optionList"
      :class="meta.class"
      :key="'lblchks'+item.value">
        <input  :id="'c'+meta.controlId"
          type="checkbox"
          :name="'c'+meta.controlId"
          :class="meta.class"
          :value="item.value"
          :checked="modelValue"
          :readonly="meta.readonly"
          :key="'chks'+item.value"
          @input="myInput"
        >
        <span>{{item.title}}</span>
    </label>
  </span>
</template>

<script>

export default {
  name: 'nf-form-check',
  model: {
    prop: 'modelValue',
    event: 'input'
  },
  props: {
    modelValue: Boolean,
    meta: {
      type: Object,
      default: () => {
        return {
          controlId: Number, // 编号，区别同一个表单里的其他控件
          controlType: Number, // 用类型编号表示type
          colName: String, // 中文名称
          isClear: {
            // isClear  连续添加时是否恢复默认值
            type: Boolean,
            default: false
          },
          // 通用
          disabled: {
            // 是否禁用
            type: Boolean,
            default: false
          },
          class: String, // 'cssTxt input_t1'
          title: String // 提示信息
        }
      }
    }
  },
  methods: {
    myInput: function (e) {
      var returnValue = event.target.checked
      var colName = this.meta.colName // event.target.getAttribute('colname')
      this.$emit('update:modelValue', returnValue) // 返回给调用者
      this.$emit('getvalue', returnValue, colName) // 返回给中间组件
    }
  }
}
</script>
