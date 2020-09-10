/** 下拉列表框，多选的那个再考虑考虑 */
<template>
  <select  :id="'c'+meta.controlId"
    :name="'c'+meta.controlId"
    :class="meta.class"
    :multiple="meta.controlType === 151"
    :colName="meta.colName"
    @change="myInput"
    >
      <option :key="-2" value="-2" >请选择</option>
      <option
        v-for="(item,index) in meta.optionList"
        :key="index"
        :value="item.value"
        :selected="modelValue==item.value">
          {{item.title}}
      </option>
    </select>
</template>

<script>

export default {
  name: 'nf-form-select',
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
            default: true
          },
          class: String, // 'cssTxt input_t1'
          title: String // 提示信息
        }
      }
    }
  },
  data: () => {
    return {
      type: {
        160: 'color'
      }
    }
  },
  methods: {
    myInput: function (e) {
      var returnValue = event.target.value
      var colName = event.target.getAttribute('colname')
      this.$emit('update:modelValue', returnValue) // 返回给调用者
      this.$emit('getvalue', returnValue, colName) // 返回给中间组件
    }
  }
}
</script>
