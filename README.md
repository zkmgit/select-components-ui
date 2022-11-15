# Author-Kay.
# Select 基于Element UI 二次封装的选择器组件

## 基本使用方法
```js
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

```

# Props Select

|  属性  |   类型  | 默认值 |  字段说明 |
| :----: | :----: | :----: |  :----:  |
| placeholder | String | 请选择 | 占位符 |
| popperClass | String | - | Select 下拉框的类名 |
| disabled | Boolean | false | 	是否禁用 |
| collapseTags | Boolean | false | 多选时是否将选中值按文字的形式展示 |
| multiple | Boolean | false | 是否多选 |
| defaultFirstOption | Boolean | false | 在输入框按下回车，选择第一个匹配项 |
| apiFn        | Funtion | () => {} | 选择器的下拉数据查询api |