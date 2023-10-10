#Vue

验证Button组件的Prop类型 ，使它只接收: primary | ghost | dashed | link | text | default ，且默认值为default。


### 方法一
```vue
<script setup>
defineProps({
  type:{
    type: String,
    validator(value) {
      if(typeof value !== 'string') return false
      return ['primary', 'ghost','dashed','link','text','default'].includes(value)
    },
  default : 'default'
  }
})
</script>

<template>
  <button>Button</button>
</template>
```


### 方法二
```vue
<script setup lang="ts">
interface ButtonProps {
  type: 'primary' | 'ghost' | 'dashed' | 'link' | 'text' | 'default'
};

withDefaults(defineProps<ButtonProps >(), {
  type: 'default'
})
</script>

<template>
  <button>Button</button>
</template>
```


### 方法三
```vue
// 你的答案
<script setup lang="ts">
defineProps({
  type: {
    type: String,
    validator(value: string){
      return ['primary', 'ghost','dashed','link','text','default'].includes(value)
    },
    default: 'default'
  }
})
</script>

<template>
  <button>Button</button>
</template>
```