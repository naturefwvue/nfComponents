/** 多选组，返回选择的value */
<template>
  <!--单选组 radio_g_s  label radio_g_t-->
  <span>
    <label role="radio" v-for="item in meta.optionList" :key="item.id">
      <input type="radio"
          :class="meta.class"
          :checked="item.check"
          :name="'c'+meta.controlId"
          :value="item.value"
          @input="myInput"
      >
      <span>{{item.title}}</span>
    </label>
  </span>
</template>

<script>

export default {
  name: 'nf-form-radio',
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
        180: 'radio', // 单选
        181: 'radios', // 单选组
        182: 'checkbox', // 复选
        183: 'checkboxs' // 多选组
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
