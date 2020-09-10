<template>
  <div class="home">
    v-for="a in 'abe'"
    <nfInput v-model="title" :meta="metaInfo"  />
    <nfHelp v-model="metaInfo" />
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue'
import nfHelp from '@/components/nf-meta-help.vue'
import nfInput from '@/components/nf-form-item.vue'

export default {
  name: 'FormHelp',
  components: {
    // nfFormItem,
    nfHelp,
    nfInput
  },
  data: () => {
    return {
      a: '11'
    }
  },
  setup () {
    // const json = require('../../public/json.json')
    // alert(json.controlId)
    const title = ref('返回json')
    const metaInfo = ref({
      controlId: 100,
      controlType: 101,
      colName: 'controlId'
    })
    // alert('setup:' + value.value)

    return {
      title,
      metaInfo
    }
  }
}
</script>
