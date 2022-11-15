<template>
  <div>
    <Select v-model="value" :apiFn="apiFn" @onChange="onChange" />
  </div>
</template>

<script>
import { Select } from './components/Select'

export default {
  name: 'App',
  components: {
    Select
  },
  data() {
    return {
      value: ''
    }
  },
  methods: {
    onChange(val, options, props) {
      console.log(val, options, props)
    },
    async apiFn() {
      return [
        { label: 'aa', value: 'aa'},
        { label: 'bb', value: 'bb'},
        { label: 'cc', value: 'cc'},
        { label: 'dd', value: 'dd'}
      ]
    } 
  }
}
</script>
