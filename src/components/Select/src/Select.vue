<template>
  <el-select v-bind="$attrs" v-model="modelValue" :popper-class="popperClass" :placeholder="placeholder" :collapse-tags="collapseTags" :multiple="multiple" :default-first-option="defaultFirstOption" clearable filterable :disabled="disabled || loading" @visible-change="onVisibleChange" @change="onChange">
    <el-option v-for="(item, index) in options" :key="item.value + '/' + item.label + '/' + index" :label="item.label" :value="item.value" :disabled="item.disabled" />
  </el-select>
</template>
<script>
import { isFunction } from 'lodash'

export default {
  name: 'Select',
  props: {
    value: {
      type: [String, Number, Array, Boolean],
      default: ''
    },
    placeholder: {
      type: String,
      default: '请选择'
    },
    popperClass: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    collapseTags: {
      type: Boolean,
      default: false
    },
    defaultFirstOption: {
      type: Boolean,
      default: false
    },
    multiple: {
      type: Boolean,
      default: false
    },
    apiFn: {
      type: Function,
      default: () => {
        return () => {}
      }
    },
  },
  computed: {
    modelValue: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  },
  data() {
    return {
      options: [],
      loading: false,
      propFields: ['placeholder', 'popperClass', 'disabled', 'collapseTags', 'defaultFirstOption', 'multiple']
    }
  },
  methods: {
    async onVisibleChange(val) {
      if (val && isFunction(this.apiFn)) {
        this.loading = true
        this.options = await this.apiFn()
        this.loading = false
      }
    },
    onChange(val) {
      const props = {}

      this.propFields.forEach(field => {
        props[field] = this[field]
      })

      this.$emit('onChange', val, this.options, props)
    }
  }
}
</script>
<style lang="scss">
.el-scrollbar .el-select-dropdown__wrap .el-select-dropdown__list {
  max-width: 400px;
}
</style>
