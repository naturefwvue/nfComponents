<template>
  <div class="about">
    <h1>This is an about page</h1>
    <nfColor v-model="value" :meta="itemcolor"/> {{value}} dd<br>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue'
import nfColor from '@/components/nf-form-color.vue'

export default {
  name: 'Home',
  components: {
    nfColor
  },
  setup () {
    const value = ref('#555555')
    const itemcolor = ref({
      controlId: 100,
      controlType: 160,
      colName: '颜色'
    })
    return {
      value,
      itemcolor
    }
  }
}
</script>
