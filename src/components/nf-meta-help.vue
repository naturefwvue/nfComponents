/** 表单meta的辅助生成工具 */
<template>
  <div class="home">
    <div><h1>表单meta生成工具</h1></div>
    <div style="background-color:#dddddd;height:600px;width:400px;float:left;">
      <table>
        <tr v-for="(item,index) in trList" :key="index">
          <td align="right">{{helpMeta[item].colName}}：
          </td>
          <td align="left">
            <nfInput :modelValue="modelValue[helpMeta[item].colName]" :meta="helpMeta[item]" @getvalue="sendValue"/>
            {{helpMeta[item].title}}
          </td>
        </tr>
      </table>
    </div>
    <div align="left" style="padding:5px;background-color:#FFFFEE;height:600px;width:400px;float:left;">
      测试：<nfInput v-model="testValue" :meta="reMeta"  /> ==》 {{testValue}}
      <div align="left" style="padding:15px;background-color:#FFEEEE;height:400px;width:400px;clear:both">
        {<br>
          <span v-for="(item, key, index) in tmpMeta" :key="index">
            <span v-if="typeof item === 'number' && !isNaN(item)">&nbsp;&nbsp;"{{key}}": {{item}}, <br></span>
            <span v-if="typeof item === 'string'">&nbsp;&nbsp;"{{key}}": "{{item}}", <br></span>
            <span v-if="typeof(item) ==='boolean'">&nbsp;&nbsp;"{{key}}": {{item}}, <br></span>
            <span v-if="typeof(item) ==='object'">
              &nbsp;&nbsp;"{{key}}": [<br>
              <span v-for="(opt, index) in item" :key="'opt'+index">&nbsp;&nbsp;&nbsp;&nbsp;{{opt}}, <br></span>
              &nbsp;&nbsp;]<br>
            </span>
          </span>
        }
      </div>
    </div>
    <div align="left" style="background-color:#EEEEFF;height:600px;width:400px;clear:both">
      {<br>
        <span v-for="(item, key, index) in reMeta" :key="index">
          <span v-if="typeof item === 'number' && !isNaN(item)">&nbsp;&nbsp;"{{key}}": {{item}}, <br></span>
          <span v-if="typeof item === 'string'">&nbsp;&nbsp;"{{key}}": "{{item}}", <br></span>
          <span v-if="typeof(item) ==='boolean'">&nbsp;&nbsp;"{{key}}": {{item}}, <br></span>
          <span v-if="typeof(item) ==='object'">
            &nbsp;&nbsp;"{{key}}": [<br>
            <span v-for="(opt, index) in item" :key="'opt'+index">&nbsp;&nbsp;&nbsp;&nbsp;{{opt}}, <br></span>
            &nbsp;&nbsp;]
          </span>
        </span>
      }
    </div>
    <div align="left" style="background-color:#EEEEEE;height:600px;width:400px;clear:both">
      {{reMeta}}
    </div>
  </div>
</template>

<script>
import nfInput from '@/components/nf-form-item.vue'

export default {
  name: 'nf-meta-help',
  components: {
    // nfFormItem,
    nfInput
  },
  model: {
    prop: 'modelValue',
    event: 'input'
  },
  props: {
    modelValue: Object
  },
  data: function () {
    return {
      ctlType: 101,
      testValue: '测试',
      helpMeta: {}, // 绑定控件的
      reMeta: { // 固定属性的
        controlId: 101,
        colName: 'abc',
        controlType: 101,
        isClear: true,
        defaultValue: '',
        autofocus: false,
        disabled: false,
        required: true,
        readonly: false,
        pattern: '',
        class: '',
        placeholder: '请输入',
        title: '',
        autocomplete: 'on',
        size: 10,
        maxlength: 10,
        min: 0,
        max: 9999,
        step: 1,
        rows: 5,
        cols: 50,
        optionKey: 'beixuan',
        optionList: []
      },
      tmpMeta: {}, // 按需生成属性的
      trList: [103],
      type: {},
      numberList: []
    }
  },
  created: function () {
    // 读取json
    const json = require('../components/metahelp.json')
    // 给data赋值
    this.helpMeta = json.helpMeta
    this.helpMeta[103].optionList = json.dic.ControlTypeList
    this.type = json.type
    this.trList = this.type[103]
    // alert(this.trList)
  },
  mounted: function () {
    var meta = this.modelValue
    // 外部数据给内部固定模板赋值
    for (var key in meta) {
      this.reMeta[key] = meta[key]
    }
    // 根据类型拼接对象
    this.tmpMeta = {}
    this.trList = this.type[meta.controlType] // 根据外部控件类型设置需要的属性
    for (var i = 0; i < this.trList.length; i += 1) {
      var item = this.trList[i]
      var key1 = this.helpMeta[item].colName
      this.tmpMeta[key1] = this.reMeta[key1]
    }
  },
  methods: {
    myInput: function (e) {
      // alert(this.aa)
      // alert('属性：' + modelValue)
      this.$emit('update:modelValue', this.aa) // 返回给调用者
    },
    sendValue: function (value, colName) {
      // 根据字段名，设置
      // alert(colName)
      if (colName === 'controlType') {
        this.trList = this.type[value]
      }
      // 给对应字段赋值
      this.reMeta[colName] = value

      // 根据类型拼接对象
      this.tmpMeta = {}
      for (var i = 0; i < this.trList.length; i += 1) {
        var item = this.trList[i]
        var key = this.helpMeta[item].colName
        this.tmpMeta[key] = this.reMeta[key]
      }
      this.$emit('update:modelValue', this.tmpMeta)
    }
  }
}
</script>
