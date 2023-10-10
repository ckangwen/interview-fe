#Vue

```vue
// 你的答案
<script setup lang='ts'>

import { h, ref } from "vue"

/**
 * Implement a functional component :
 * 1. Render the list elements (ul/li) with the list data
 * 2. Change the list item text color to red when clicked.
*/
const ListComponent = (props,{emit}) => {
  return h('ul',props.list.map(({name},index)=>{
    return h('li',{
      style:{
        color: props['active-index'] === index ? 'red' : ''
      },
      onclick:()=>emit('toggle',index)
    },name)
  }))
}

const list = [{
  name: "John",
}, {
  name: "Doe",
}, {
  name: "Smith",
}]

const activeIndex = ref(0)

function toggle(index: number) {
  activeIndex.value = index
}

</script>

<template>
  <list-component
    :list="list"
    :active-index="activeIndex"
    @toggle="toggle"
  />
</template>

```