/** 上传图片和文件，具体功能未实现，等待第三方UI */
<template>
  <span>
    <span v-if="meta.controlType <= 219">
       <input :id="'c' + meta.controlId"
        type="file"
        :name="'c' + meta.controlId"
        :value="modelValue"
        :disabled="meta.disabled"
        :class="meta.class"
        :title="meta.title"
        :placeholder="meta.placeholder"
        :readonly="meta.readonly"
        :autocomplete="meta.autocomplete"
        @input="myInput"
        :key="'ckey_'+meta.controlId">
    </span>
  </span>
</template>

<script>

export default {
  name: 'nf-form-upload',
  model: {
    prop: 'modelValue',
    event: 'input'
  },
  props: {
    modelValue: String,
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
          required: { // 必填
            type: Boolean,
            default: false
          },
          pattern: String, // 用正则做验证。
          class: String, // 'cssTxt input_t1'
          title: String, // 提示信息
          // 多行文本
          rows: Number, // 行数
          cols: Number, // 列数
          // 文本框类
          placeholder: String,
          readonly: { // 只读
            type: Boolean,
            default: false
          },
          autocomplete: { // off
            type: String,
            default: 'on'
          }
        }
      }
    }
  },
  methods: {
    myInput: function (e) {
      var returnValue = event.target.value
      var colName = this.meta.colName // event.target.getAttribute('colname')
      this.$emit('update:modelValue', returnValue) // 返回给调用者
      this.$emit('getvalue', returnValue, colName) // 返回给中间组件
    }
  }
}
</script>
