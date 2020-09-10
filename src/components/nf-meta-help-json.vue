/** 提供meta生成工具的json */
<template>
  <span :value="modelValue"></span>
</template>

<script>

export default {
  name: 'nf-meta-help-json',
  model: {
    prop: 'modelValue'
  },
  props: {
    modelValue: Object
  },
  data: function () {
    return {
      aa: {
        controlId: 101,
        controlType: 100,
        colName: 'abc',
        isClear: true,
        disabled: false,
        required: true,
        class: '1',
        title: '1',
        rows: 5,
        cols: 50,
        placeholder: '请输入',
        readonly: false
      }
    }
  },
  created: function () {
    // alert('created:' + this.aa)
    this.$emit('update:modelValue', this.aa) // 返回给调用者
  }
}
</script>
