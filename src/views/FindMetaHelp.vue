<template>
  <div class="home">
    <nfInput v-model="value" :meta="metaInfo"  /> {{value}}
    <nfHelp v-model="metaInfo" />
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue'
import nfHelp from '@/components/nf-meta-findhelp.vue'
import nfInput from '@/components/nf-form-item.vue'

export default {
  name: 'FormHelp',
  components: {
    // nfFormItem,
    nfHelp,
    nfInput
  },
  setup () {
    const value = ref('')
    const metaInfo = ref({
      controlId: 100,
      controlType: 101,
      colName: 'controlId',
      title: '',
      autocomplete: 'on',
      size: 10,
      maxlength: 10,
      optionKey: '',
      optionList: [],
      findKind: '401',
      tdCount: 1
    })

    return {
      value,
      metaInfo
    }
  }
}
</script>
