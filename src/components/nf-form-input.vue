/** 文本类的，text、密码、url、邮件等 */
<template>
  <span>
    <input :id="'c' + meta.controlId"
    :type="type[meta.controlType]"
    :name="'c' + meta.controlId"
    :value="modelValue"
    :disabled="meta.disabled"
    :readonly="meta.readonly"
    :class="meta.class"
    :placeholder="meta.placeholder"
    :title="meta.title"
    :size="meta.size"
    :maxlength="meta.maxlength"
    :autocomplete="meta.autocomplete"
    :list="meta.optionKey"
    @input="myInput"
    :key="'ckey_'+meta.controlId">
    <!--文本框的备选项-->
    <datalist v-if="typeof(meta.optionKey)!=='undefined'" :id="meta.optionKey">
      <option :key="item.value" v-for="item in meta.optionList" :label="item.value" :value="item.title" />
    </datalist>
  </span>
</template>

<script>

export default {
  name: 'nf-form-input',
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
          // 通用
          controlId: Number, // 编号，区别同一个表单里的其他控件
          colName: String, // 字段名称
          controlType: Number, // 用类型编号表示type
          isClear: {
            // isClear  连续添加时是否恢复默认值
            type: Boolean,
            default: false
          },
          defaultValue: String, // 默认值
          autofocus: { // 是否自动获得焦点
            type: Boolean,
            default: false
          },
          disabled: {
            // 是否禁用
            type: Boolean,
            default: false
          },
          required: { // 必填
            type: Boolean,
            default: true
          },
          readonly: { // 只读
            type: Boolean,
            default: false
          },
          pattern: String, // 用正则做验证。
          class: String, // 'cssTxt input_t1'
          placeholder: String,
          title: String, // 提示信息
          size: Number, // 字符宽度
          maxlength: Number, // 最大字符数
          autocomplete: { // off
            type: String,
            default: 'on'
          },
          optionKey: String, // 备选文字标识
          optionItem: Object // 备选的选项
        }
      }
    }
  },
  data: () => {
    return {
      type: {
        100: 'textarea', // 多行文本框
        101: 'text', // 单行文本框
        102: 'password', // 密码
        103: 'tel', // 电话
        104: 'email', // 电子邮件
        105: 'url', // url
        106: 'search', // 搜索
        107: 'text', // 当前登录人
        120: 'fulltext', // 富文本编辑器
        131: 'number', // 数字
        132: 'range', // 滑块
        140: 'date', // 日期
        141: 'datetime-local', // 日期时间
        142: 'time', // 时间
        143: 'month', // 年月
        144: 'week', // 年周
        150: 'file', // 上传文件
        151: 'file', // 上传图片
        160: 'color', // 颜色
        170: 'text', // 弹窗选择记录
        180: 'checkbox', // 勾选
        182: 'checkboxs', // 多选组
        183: 'radios', // 单选组
        190: 'select', // 下拉列表框 单选
        191: 'selects', // 列表框 多选
        192: 'selectMore' // 联动下拉列表框
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
