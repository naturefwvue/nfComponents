<template>
  <div class="home">
    <h1>查询演示22</h1>
    <div style="background-color:#dddddd;height:600px;width:100px;float:left;">
      <a href="#" @click="myClick('companyForm')">公司信息</a> <br>
      <a href="#" @click="myClick('personForm')">员工信息</a>
    </div>
    <div style="background-color:#eee;height:600px;width:900px;float:left;">{{getName(1,4)}}
      <table rules='all' border="1">
        <tr v-for="row in rowCount" :key="row">
          <td v-for="col in colCount * 2" :key="col">
            <span v-if="col % 2 === 1 && ((row-1)*3 + Math.floor(col / 2)) < 10">
              {{(row-1)*3 + Math.floor(col / 2)}}-
              {{metaArr[(row-1)*3 + Math.floor(col / 2)].title}}：
            </span>
            <span v-else-if="col % 2 === 0 && ((row-1)*3 + Math.floor(col / 2)-1) < 10" >{{(row-1)*3 + Math.floor(col / 2)-1}}+
              <nfInput :aa="((row-1)*3 + Math.floor(col / 2)-1)" v-model="modelValue[getName(row,col)]" :meta="metaArr[(row-1)*3 + Math.floor(col / 2)-1]" />
            </span>
          </td>
        </tr>
      </table>
      <table>
        <tr v-for="(item,index) in metaInfo" :key="index">
          <td align="right">{{item.title}}：
          </td>
          <td align="left">{{item.FindKind}}
            <nfInput v-model="modelValue[item.colName]" :meta="item" />
          </td>
        </tr>
      </table>
    </div>
    <div align="left" style="background-color:#EEEEFF;height:600px;width:300px;clear:both">
      {{valueArr}}<br>
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
    const json = require('./FindDemo.json') // 加载meta信息，json格式
    const modelValue = ref({}) // 放数据的model
    const metaInfo = ref(json.companyForm) // 表单需要的meta信息
    const rowCount = ref(1) // 行数，遍历用，计算得出
    const colCount = ref(3) // 列数，遍历用，直接给定
    const tdCount = ref(1) // 控件数，遍历用
    const metaArr = ref([]) // 数组形式的meta
    const colNameArr = ref([]) // 数组形式的字段名
    const valueArr = ref([''])
    const getName = (row, col) => {
      return colNameArr.value[(row - 1) * 3 + Math.floor(col / 2) - 1]
    }
    const myClick = (key) => {
      // 更换表单的meta
      metaInfo.value = json[key]
      // 创建model
      modelValue.value = {}
      rowCount.value = 0
      for (var k in metaInfo.value) {
        var item = metaInfo.value[k]
        modelValue.value[item.colName] = ''
        tdCount.value += 1
        metaArr.value.push(item)
        colNameArr.value.push(item.colName)
        // colNameArr.value.push(item.colName)
        valueArr.value.push('')
        valueArr.value.push('')
      }
      // 计算行数
      rowCount.value = Math.ceil(tdCount.value / colCount.value)
      // alert(rowCount.value)
    }
    myClick('companyForm')
    return {
      modelValue,
      metaInfo,
      rowCount,
      colCount,
      tdCount,
      metaArr,
      colNameArr,
      valueArr,
      myClick,
      getName
    }
  }
}
</script>
