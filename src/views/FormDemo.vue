<template>
  <div class="home">
    <h1>表单演示</h1>
    <div style="background-color:#dddddd;height:600px;width:100px;float:left;">
      <a href="#" @click="myClick('companyForm')">公司信息</a> <br>
      <a href="#" @click="myClick('personForm')">员工信息</a>
    </div>
    <div style="background-color:#eee;height:600px;width:400px;float:left;">
      <table>
        <tr v-for="(item,index) in metaInfo" :key="index">
          <td align="right">{{item.title}}：
          </td>
          <td align="left">
            <nfInput v-model="modelValue[item.colName]" :meta="item" />
          </td>
        </tr>
      </table>
    </div>
    <div align="left" style="background-color:#EEEEFF;height:600px;width:300px;float:left;">
      {<br>
        <span v-for="(item, key, index) in modelValue" :key="index">
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
    <div style="clear:both">
      {{modelValue}}
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
// import nfHelp from '@/components/nf-meta-help.vue'
import nfInput from '@/components/nf-form-item.vue'

export default {
  name: 'FormDemo',
  components: {
    // nfHelp,
    nfInput
  },
  setup () {
    const json = require('./FormDemo.json') // 加载meta信息，json格式
    const modelValue = ref({}) // 放数据的model
    const metaInfo = ref(json.companyForm) // 表单需要的meta信息
    const myClick = (key) => {
      // 更换表单的meta
      metaInfo.value = json[key]
      // 创建model
      modelValue.value = {}
      for (var k in metaInfo.value) {
        var item = metaInfo.value[k]
        modelValue.value[item.colName] = ''
      }
    }
    myClick('companyForm')
    return {
      modelValue,
      metaInfo,
      myClick
    }
  }
}
</script>
