#Vue

### 组件作用域 CSS
当 `<style>` 标签带有 `scoped` attribute 的时候，它的 CSS 只会影响当前组件的元素


### 子组件的根元素

使用 `scoped` 后，父组件的样式将不会渗透到子组件中。

**深度选择器**
处于 `scoped` 样式中的选择器如果想要做更“深度”的选择，也即：影响到子组件，可以使用 `:deep()` 这个伪类：
```css
<style scoped>
.a :deep(.b) {
  /* ... */
}
</style>
```
上面的代码会被编译成：
```css
.a[data-v-f3f3eg9] .b {
  /* ... */
}
```

**插槽选择器**
默认情况下，作用域样式不会影响到 <slot/> 渲染出来的内容，因为它们被认为是父组件所持有并传递进来的。
使用 `:slotted` 伪类以明确地将插槽内容作为选择器的目标：
```css
<style scoped>
:slotted(div) {
  color: red;
}
</style>
```

**全局选择器**
如果想让其中一个样式规则应用到全局，比起另外创建一个 `<style>`，可以使用 `:global` 伪类来实现
```css
<style scoped>
:global(.red) {
  color: red;
}
</style>
```

### CSS Module
一个 `<style module>` 标签会被编译为 CSS Modules 并且将生成的 CSS class 作为 `$style` 对象暴露给组件：
```css
<template>
  <p :class="$style.red">This should be red</p>
</template>

<style module>
.red {
  color: red;
}
</style>
```

得出的 class 将被哈希化以避免冲突，实现了同样的将 CSS 仅作用于当前组件的效果。



**自定义注入名称**
你可以通过给 module attribute 一个值来自定义注入 class 对象的属性名：
```css
<template>
  <p :class="classes.red">red</p>
</template>

<style module="classes">
.red {
  color: red;
}
</style>
```


**与组合式 API 一同使用**
可以通过 useCssModule API 在 setup() 和 `<script setup>` 中访问注入的 class。
对于使用了自定义注入名称的 `<style module>` 块，`useCssModule` 接收一个匹配的 module attribute 值作为第一个参数：
```css
import { useCssModule } from 'vue'

// 在 setup() 作用域中...
// 默认情况下, 返回 <style module> 的 class
useCssModule()

// 具名情况下, 返回 <style module="classes"> 的 class
useCssModule('classes')
```

### CSS中的`v-bind`
单文件组件的 `<style>` 标签支持使用 `v-bind` CSS 函数将 CSS 的值链接到动态的组件状态：
```vue
<template>
  <div class="text">hello</div>
</template>

<script>
export default {
  data() {
    return {
      color: 'red'
    }
  }
}
</script>

<style>
.text {
  color: v-bind(color);
}
</style>
```


这个语法同样也适用于 `<script setup>`，且支持 JavaScript 表达式 (需要用引号包裹起来)：
```vue
<script setup>
const theme = {
  color: 'red'
}
</script>

<template>
  <p>hello</p>
</template>

<style scoped>
p {
  color: v-bind('theme.color');
}
</style>
```

实际的值会被编译成哈希化的 CSS 自定义属性，因此 CSS 本身仍然是静态的。自定义属性会通过内联样式的方式应用到组件的根元素上，并且在源值变更的时候响应式地更新。