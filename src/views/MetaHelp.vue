<template>
  <div class="home">
    <div><h1>表单meta生成工具1</h1></div>
    <div style="background-color:#dddddd;height:600px;width:400px;float:left;">
        <table>
        <tr v-for="item in metaInfo" :key="item.controlId">
            <td align="right">{{item.colName}}：
            </td>
            <td align="left"><nfInput autofocus v-model="metaValue[item.colName]" :meta="item" @input="myCilck" />
            </td>
        </tr>
        </table>
    </div>
    <div style="background-color:#EEEEEE;height:600px;width:400px;float:left;">
        <nfInput v-model="title" :meta="metaValue" />{{title}}<br>
        <textarea :value="metaValueString" rows="25" cols="50"></textarea>
        {{metaValue}}
    </div>
    <div style="background-color:#EEEEEE;height:600px;width:400px;clear:both">
        {<br>
          <span v-for="(item, key, index) in metaValue" :key="index">
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
  </div>
</template>

<script>
// @ is an alias to /src
import { ref, computed, watch } from 'vue'
import nfInput from '@/components/nf-form-item.vue'

export default {
  name: 'FormHelp',
  components: {
    // nfFormItem,
    nfInput
  },
  data: () => {
    return {
      a: '11'
    }
  },
  setup () {
    const title = ref('2')
    const value = ref('1,3')

    // 控件类型的下拉列表框
    const ControlTypeList = [{
      id: 100, title: '多行文本框'
    }, {
      id: 101, title: '单行文本框'
    }, {
      id: 102, title: '密码框'
    }, {
      id: 103, title: '电话'
    }, {
      id: 104, title: '电子邮件'
    }, {
      id: 105, title: 'url'
    }, {
      id: 106, title: '搜索'
    }, {
      id: 107, title: '当前登录人'
    }, {
      id: 120, title: '富文本编辑器'
    }, {
      id: 131, title: '数字'
    }, {
      id: 132, title: '滑块'
    }, {
      id: 140, title: '日期'
    }, {
      id: 141, title: '日期时间'
    }, {
      id: 142, title: '时间'
    }, {
      id: 143, title: '年月'
    }, {
      id: 144, title: '年周'
    }, {
      id: 150, title: '上传文件'
    }, {
      id: 151, title: '上传图片'
    }, {
      id: 160, title: '颜色'
    }, {
      id: 170, title: '弹窗选择记录'
    }, {
      id: 180, title: '勾选'
    }, {
      id: 182, title: '多选组'
    }, {
      id: 183, title: '单选组'
    }, {
      id: 190, title: '下拉列表框'
    }, {
      id: 191, title: '列表框'
    }, {
      id: 192, title: '联动下拉列表框'
    }]
    // 生成工具需要的meta
    const metaInfo = ref([{
      controlId: 101,
      controlType: 101,
      colName: 'controlId'
    },
    {
      controlId: 102,
      controlType: 190,
      colName: 'controlType',
      options: ControlTypeList
    },
    {
      controlId: 103,
      controlType: 101,
      colName: 'colName'
    },
    {
      controlId: 104,
      controlType: 180,
      colName: 'isClear',
      option: {
        value: 1,
        checked: false,
        title: '添加新纪录是否清空？'
      }
    },
    {
      controlId: 105,
      controlType: 180,
      colName: 'disabled',
      option: {
        value: 1,
        checked: false,
        title: '是否禁用？'
      }
    },
    {
      controlId: 106,
      controlType: 180,
      colName: 'required',
      option: {
        value: 1,
        checked: true,
        title: '是否必填？'
      }
    },
    {
      controlId: 107,
      controlType: 101,
      colName: 'pattern'
    },
    {
      controlId: 108,
      controlType: 101,
      colName: 'class'
    },
    {
      controlId: 109,
      controlType: 101,
      colName: 'title'
    },
    {
      controlId: 110,
      controlType: 131,
      colName: 'rows'
    },
    {
      controlId: 111,
      controlType: 131,
      colName: 'cols'
    },
    {
      controlId: 112,
      controlType: 101,
      colName: 'placeholder'
    },
    {
      controlId: 113,
      controlType: 180,
      colName: 'readonly',
      option: {
        value: 1,
        checked: false,
        title: '是否只读？'
      }
    },
    {
      controlId: 114,
      controlType: 131,
      colName: 'size'
    },
    {
      controlId: 115,
      controlType: 131,
      colName: 'maxlength'
    },
    {
      controlId: 116,
      controlType: 183,
      colName: 'autocomplete',
      options: [{
        value: 'on',
        title: '跟踪'
      }, {
        value: 'off',
        title: '关闭'
      }]
    },
    {
      controlId: 117,
      controlType: 101,
      colName: 'optionKey'
    },
    {
      controlId: 118,
      controlType: 200,
      colName: 'optionItem'
    }
    ])
    const metaValue = ref({
      controlId: 101,
      controlType: 100,
      colName: 'abc',
      isClear: true,
      disabled: false,
      required: true,
      pattern: '1',
      class: '1',
      title: '1',
      rows: 5,
      cols: 50,
      placeholder: '请输入',
      readonly: false,
      size: 10,
      maxlength: 10,
      autocomplete: 'on',
      optionKey: 'beixuan',
      optionItem: []
    })
    const metaValueString = ref('33')
    watch(() => metaValue.value.colName,
      (val) => {
        console.log(`count is ${val}`)
        metaValueString.value = `count is ${val}`
      })
    const doubleCount = computed(() => metaValue.value.controlId * 2)
    const myCilck = () => {
      var str = '{' + '\n'
      str += '  controlId:' + metaValue.value.controlId + ',\n'
      str += '  controlType:' + metaValue.value.controlType + ',\n'
      str += '  colName:\'' + metaValue.value.colName + '\',\n'
      str += '  isClear:' + metaValue.value.isClear + ',\n'
      str += '  disabled:' + metaValue.value.disabled + ',\n'
      str += '  required:' + metaValue.value.required + ',\n'
      str += '  pattern:\'' + metaValue.value.pattern + '\',\n'
      str += '  class:\'' + metaValue.value.class + '\',\n'
      str += '  title:\'' + metaValue.value.title + '\',\n'
      str += '  rows:' + metaValue.value.rows + ',\n'
      str += '  cols:' + metaValue.value.cols + ',\n'
      str += '  placeholder:\'' + metaValue.value.placeholder + '\',\n'
      str += '  readonly:' + metaValue.value.readonly + ',\n'
      str += '  size:' + metaValue.value.size + ',\n'
      str += '  maxlength:' + metaValue.value.maxlength + ',\n'
      str += '  autocomplete:\'' + metaValue.value.autocomplete + '\',\n'
      str += '  optionKey:\'' + metaValue.value.optionKey + '\',\n'
      var optItem = []
      for (var key in metaValue.value.optionItem) {
        var item = metaValue.value.optionItem[key]
        optItem.push('    { value:' + item.value + '  title:\'' + item.title + ' }')
      }
      optItem = '[\n' + optItem.join(',\n') + '\n  ]'
      str += '  optionItem:' + optItem + ',\n'
      str += '}' + '\n'
      metaValueString.value = str
    }
    myCilck()
    return {
      title,
      value,
      metaInfo,
      metaValue,
      metaValueString,
      doubleCount,
      myCilck
    }
  }
}
</script>
