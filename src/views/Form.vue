<template>
  <div class="home">
       表单组件
      <nfColor v-model="title" :meta="itemcolor"/> {{title}} dd<br>
      <nfInput v-model="value" :meta="itemcolor"/> {{value}} <br>
      勾选：<nfCheck v-model="value" :meta="metaCheck"/> {{value}} <br>
      多选：<nfChecks v-model="value" :meta="metaChecks"/> {{value}} <br>
      下拉：<nfSelect v-model="value" :meta="metaSelect"/> {{value}} <br>
      <div v-for="item in metaInfo" :key="item.controlId">
        {{item.colName}}：<nfInput v-model="metaValue[item.colName]" :meta="item"  />
      </div>
      {{metaValue}}
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue'
import nfInput from '@/components/nf-form-item.vue'
// import nfInput from '@/components/nf-form-input.vue'
import nfColor from '@/components/nf-form-color.vue'
import nfCheck from '@/components/nf-form-check.vue'
import nfChecks from '@/components/nf-form-checks.vue'
import nfSelect from '@/components/nf-form-select.vue'

export default {
  name: 'Home',
  components: {
    // nfFormItem,
    nfInput,
    nfCheck,
    nfChecks,
    nfSelect,
    nfColor
  },
  setup () {
    const title = ref('2')
    const value = ref('2,3')

    const metaInfo = ref([{
      controlId: 101,
      controlType: 101,
      colName: 'controlId'
    },
    {
      controlId: 102,
      controlType: 101,
      colName: 'controlType'
    },
    {
      controlId: 101,
      controlType: 100,
      colName: 'colName'
    }])
    const metaValue = ref({
      controlId: 101,
      controlType: 100,
      colName: 'abc'
    })
    const meta = ref({
      controlId: 100,
      controlType: 101,
      colName: 'abc'
    })
    const itemcolor = ref({
      controlId: 100,
      controlType: 140,
      colName: '颜色',
      list: [{
        id: 1,
        check: false,
        name: 'a'
      },
      {
        id: 2,
        check: false,
        name: 'b'
      }]
    })
    const metaCheck = ref({
      controlId: 100,
      controlType: 180,
      colName: '勾选',
      option: {
        value: 1,
        checked: false,
        title: '你同意吗？'
      }
    })
    const metaChecks = ref({
      controlId: 100,
      controlType: 140,
      colName: '颜色',
      options: [{
        id: 1,
        checked: false,
        title: 'a'
      },
      {
        id: 2,
        checked: false,
        title: 'b'
      },
      {
        id: 3,
        checked: false,
        title: 'v'
      }]
    })
    const metaSelect = ref({
      controlId: 100,
      controlType: 190,
      colName: '下拉列表框',
      options: [{
        id: 1,
        checked: false,
        title: 'a'
      },
      {
        id: 2,
        checked: false,
        title: 'b'
      }]
    })
    const meta4 = ref({
      controlId: 153,
      controlType: 153,
      colName: 'abc',
      list: [{
        id: 1,
        check: false,
        name: 'a'
      },
      {
        id: 2,
        check: true,
        name: 'b'
      }]
    })

    return {
      title,
      value,
      meta,
      meta4,
      itemcolor,
      metaInfo,
      metaCheck,
      metaChecks,
      metaSelect,
      metaValue
    }
  }
}
</script>
