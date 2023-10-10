#Vue 


### 全局API
#### 全部API应用示例

**全局API行为**
Vue2废弃`Vue.component`, `Vue.directive`, `Vue.mixin`
因为这样会影响到全部的根实例
Vue3使用了`createApp`
任何全局改变 Vue 行为的 API 现在都会移动到应用实例上

**`Vue.property`替换成`app. globalProperties`**

**`config.productionTip` 移除**
- 在 Vue 3.x 中，“使用生产版本”提示仅在使用“dev + full build”时才会显示
- CLI 或脚手架已经正确地配置了生产环境，所以本提示将不再出现

**`config.ignoredElements` 替换为 `config.isCustomElement`**
- 重命名可以更好地传达它的意图
- 新选项接受一个函数，相比旧的字符串或正则表达式来说能提供更高的灵活性


**`Vue.extend` 移除**
- 没有组件构造器的概念了
- 组件继承推荐使用组合式API

**provide/inject**

---

#### 全局 API Treeshaking
Vue 2.x 中的这些全局 API 受此更改的影响：

- `Vue.nextTick`
- `Vue.observable` (用 `Vue.reactive` 替换)
- `Vue.version`
- `Vue.compile` (仅完整构建版本)
- `Vue.set` (仅兼容构建版本)
- `Vue.delete` (仅兼容构建版本)

---

### 模板指令

#### v-model
- **非兼容**：用于自定义组件时，`v-model` prop 和事件默认名称已更改：
    - prop：`value` -> `modelValue`；
    - 事件：`input` -> `update:modelValue`；
- **非兼容**：`v-bind` 的 `.sync` 修饰符和组件的 `model` 选项已移除，可在 `v-model` 上加一个参数代替；
- **新增**：现在可以在同一个组件上使用多个 `v-model` 绑定；
- **新增**：现在可以自定义 `v-model` 修饰符。

---

#### `key` 使用变化
- **新增**：对于 `v-if`/`v-else`/`v-else-if` 的各分支项 `key` 将不再是必须的，因为现在 Vue 会自动生成唯一的 `key`。
    - **非兼容**：如果你手动提供 `key`，那么每个分支必须使用唯一的 `key`。你将不再能通过故意使用相同的 `key` 来强制重用分支。
- **非兼容**：`<template v-for>` 的 `key` 应该设置在 `<template>` 标签上 (而不是设置在它的子节点上)。

---

#### `v-if`和`v-for`优先级
- **非兼容**：两者作用于同一个元素上时，`v-if` 会拥有比 `v-for` 更高的优先级。


---

#### `v-bind` 合并行为

- 不兼容：v-bind 的绑定顺序会影响渲染结果。
Vue2: 独立 attribute 总是会覆盖 object 中的绑定
Vue3: 绑定的声明顺序将决定它们如何被合并，后面声明的 attribute 会覆盖 前面的

---

#### `v-on.native` 移除

- v-on 的 .native 修饰符已被移除

Vue2:
默认情况下，传递给带有 v-on 的组件的事件监听器只能通过 this.$emit 触发。要将原生 DOM 监听器添加到子组件的根元素中，可以使用 .native 修饰符：

Vue3:
v-on 的 .native 修饰符已被移除。同时，新增的 emits 选项允许子组件定义真正会被触发的事件。

因此，对于子组件中未被定义为组件触发的所有事件监听器，Vue 现在将把它们作为原生事件监听器添加到子组件的根元素中 (除非在子组件的选项中设置了 inheritAttrs: false)

---

### 组件

#### 函数式组件

- 2.x 中函数式组件带来的性能提升在 3.x 中已经可以忽略不计，因此我们建议只使用有状态的组件
- 函数式组件只能由接收 `props` 和 `context` (即：`slots`、`attrs`、`emit`) 的普通函数创建
- **非兼容**：`functional` attribute 已从单文件组件 (SFC) 的 `<template>` 中移除
- **非兼容**：`{ functional: true }` 选项已从通过函数创建的组件中移除

Vue2:
单文件
```js
// Vue 2 函数式组件示例
export default {
  functional: true,
  props: ['level'],
  render(h, { props, data, children }) {
    return h(`h${props.level}`, data, children)
  }
}

```

```vue
<!-- Vue 2 结合 <template> 的函数式组件示例 -->
<template functional>
  <component
    :is="`h${props.level}`"
    v-bind="attrs"
    v-on="listeners"
  />
</template>

<script>
export default {
  props: ['level']
}
</script>

```

Vue3:
通过函数创建组件
```js
import { h } from 'vue'

const DynamicHeading = (props, context) => {
  return h(`h${props.level}`, context.attrs, context.slots)
}

DynamicHeading.props = ['level']

export default DynamicHeading

```

---

#### 异步组件
- 新的 `defineAsyncComponent` 助手方法，用于显式地定义异步组件
- `component` 选项被重命名为 `loader`
- Loader 函数本身不再接收 `resolve` 和 `reject` 参数，且必须返回一个 Promise

> https://v3-migration.vuejs.org/zh/breaking-changes/async-components.html

---

#### emits 选项

Vue 3 现在提供一个 emits 选项，和现有的 props 选项类似。这个选项可以用来定义一个组件可以向其父组件触发的事件。


---

### 渲染函数

#### 渲染函数API
此更改不会影响 `<template>` 用户。

以下是更改的简要总结：

- `h` 现在是全局导入，而不是作为参数传递给渲染函数
- 更改渲染函数参数，使其在有状态组件和函数组件的表现更加一致
- VNode 现在有一个扁平的 prop 结构

**2.x 语法**
在 2.x 中，`render` 函数会自动接收 `h` 函数 (它是 `createElement` 的惯用别名) 作为参数：


``` js
// Vue 2 渲染函数示例
export default {
  render(h) {
    return h('div')
  }
}
```

**3.x 语法**
在 3.x 中，`h` 函数现在是全局导入的，而不是作为参数自动传递。

``` js
// Vue 3 渲染函数示例
import { h } from 'vue'

export default {
  render() {
    return h('div')
  }
}
```


---

#### 插槽统一

此更改统一了 3.x 中的普通插槽和作用域插槽。
以下是变化的变更总结：

- `this.$slots` 现在将插槽作为函数公开
- **非兼容**：移除 `this.$scopedSlots`

**2.x 语法**
当使用渲染函数，即 `h` 时，2.x 曾经在内容节点上定义 `slot` 数据 property。


``` js
// 2.x 语法
h(LayoutComponent, [
  h('div', { slot: 'header' }, this.header),
  h('div', { slot: 'content' }, this.content)
])
```

此外，可以使用以下语法引用作用域插槽：

``` js
// 2.x 语法
this.$scopedSlots.header
```

**3.x 语法**

在 3.x 中，插槽以对象的形式定义为当前节点的子节点：

``` js
// 3.x Syntax
h(LayoutComponent, {}, {
  header: () => h('div', this.header),
  content: () => h('div', this.content)
})
```

当你需要以编程方式引用作用域插槽时，它们现在被统一到 `$slots` 选项中了。


``` js
// 2.x 语法
this.$scopedSlots.header

// 3.x 语法
this.$slots.header()
```

---

#### $listeners 合并到 $attrs

- `$listeners` 对象在 Vue 3 中已被移除。事件监听器现在是 `$attrs` 的一部分

---

#### $attrs 包含 class & style

- `$attrs` 现在包含了所有传递给组件的 attribute，包括 `class` 和 `style`

---

### 移除的APIs

#### 按键修饰符

- 不再支持使用数字 (即键码) 作为 v-on 修饰符
- 不再支持 config.keyCodes

在 Vue 2 中，`keyCodes` 可以作为修改 `v-on` 方法的一种方式。

``` vue
<!-- 键码版本 -->
<input v-on:keyup.13="submit" />

<!-- 别名版本 -->
<input v-on:keyup.enter="submit" />
```

此外，也可以通过全局的 `config.keyCodes` 选项定义自己的别名。


``` js
Vue.config.keyCodes = {
  f1: 112
}
```


``` vue
<!-- 键码版本 -->
<input v-on:keyup.112="showHelpText" />

<!-- 自定义别名版本 -->
<input v-on:keyup.f1="showHelpText" />
```

从 `KeyboardEvent.keyCode` 已被废弃开始，Vue 3 继续支持这一点就不再有意义了。因此，现在建议对任何要用作修饰符的键使用 kebab-cased (短横线) 名称。


``` vue
<!-- Vue 3 在 v-on 上使用按键修饰符 -->
<input v-on:keyup.page-down="nextPage">

<!-- 同时匹配 q 和 Q -->
<input v-on:keypress.q="quit">
```

---
#### 事件 API

- `$on`，`$off` 和 `$once` 实例方法已被移除，组件实例不再实现事件触发接口
> 在 2.x 中，Vue 实例可用于触发由事件触发器 API 通过指令式方式添加的处理函数 ($on，$off 和 $once)。这可以用于创建一个事件总线，以创建在整个应用中可用的全局事件监听器


---

#### 过滤器

- 从 Vue 3.0 开始，过滤器已移除，且不再支持

---


#### $children
- `$children` 实例 property 已从 Vue 3.0 中移除，不再支持



---

### 其他改动


#### 自定义指令

指令的钩子函数已经被重命名，以更好地与组件的生命周期保持一致。
额外地，`expression` 字符串不再作为 `binding` 对象的一部分被传入。

在 Vue 2 中，自定义指令通过使用下列钩子来创建，以对齐元素的生命周期，它们都是可选的：
- **bind** - 指令绑定到元素后调用。只调用一次。
- **inserted** - 元素插入父 DOM 后调用。
- **update** - 当元素更新，但子元素尚未更新时，将调用此钩子。
- **componentUpdated** - 一旦组件和子级被更新，就会调用这个钩子。
- **unbind** - 一旦指令被移除，就会调用这个钩子。也只调用一次。


在 Vue 3 中，我们为自定义指令创建了一个更具凝聚力的 API。正如你所看到的，它们与我们的组件生命周期方法有很大的不同，即使钩子的目标事件十分相似。我们现在把它们统一起来了：
- **created** - 新增！在元素的 attribute 或事件监听器被应用之前调用。
- bind → **beforeMount**
- inserted → **mounted**
- **beforeUpdate**：新增！在元素本身被更新之前调用，与组件的生命周期钩子十分相似。
- update → 移除！该钩子与 `updated` 有太多相似之处，因此它是多余的。请改用 `updated`。
- componentUpdated → **updated**
- **beforeUnmount**：新增！与组件的生命周期钩子类似，它将在元素被卸载之前调用。
- unbind -> **unmounted**


---

#### Data 选项

- **非兼容**：组件选项 `data` 的声明不再接收纯 JavaScript `object`，而是接收一个 `function`。
- **非兼容**：当合并来自 mixin 或 extend 的多个 `data` 返回值时，合并操作现在是浅层次的而非深层次的 (只合并根级属性)。

---

#### Mount API 的改变

Vue2：当挂载一个具有 template 的应用时，被渲染的内容会替换我们要挂载的目标元素。
Vue3：被渲染的应用会作为子元素插入，从而替换目标元素的 innerHTML。

---

#### Props 的默认函数访问 this

- 生成 prop 默认值的工厂函数不再能访问 `this`
- 组件接收到的原始 prop 将作为参数传递给默认函数
- inject API 可以在默认函数中使用

---

#### Transition class 名更改

- 过渡类名 `v-enter` 修改为 `v-enter-from`、过渡类名 `v-leave` 修改为 `v-leave-from`


Vue2
```css
.v-enter,
.v-leave-to {
  opacity: 0;
}

.v-leave,
.v-enter-to {
  opacity: 1;
}

```

Vue3
```css
.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-leave-from,
.v-enter-to {
  opacity: 1;
}

```

![](https://v3-migration.vuejs.org/images/transitions.svg)


---

#### Transition 作为根节点

当使用 `<transition>` 作为根结点的组件从外部被切换时将不再触发过渡效果


在 Vue 2 中，通过使用 `<transition>` 作为一个组件的根节点，过渡效果存在从组件外部触发的可能性：


``` vue
<!-- 模态组件 -->
<template>
  <transition>
    <div class="modal"><slot/></div>
  </transition>
</template>
```


``` vue
<!-- 用法 -->
<modal v-if="showModal">hello</modal>
```

**切换 `showModal` 的值将会在模态组件内部触发一个过渡效果**。

这是无意为之的，并不是设计效果。一个 `<transition>` 原本是希望被其子元素触发的，而不是 `<transition>` 自身。

这个怪异的现象现在被移除了。

---

#### TransitionGroup 不再默认渲染根节点

`<transition-group>` 不再默认渲染根元素，但仍然可以用 tag attribute 创建根元素。

在 Vue 2 中，`<transition-group>` 像其它自定义组件一样，需要一个根元素。默认的根元素是一个 `<span>`，但可以通过 `tag` attribute 定制。


``` vue
<transition-group tag="ul">
  <li v-for="item in items" :key="item">
    {{ item }}
  </li>
</transition-group>
```

在 Vue 3 中，我们有了片段的支持，因此组件不再需要根节点。所以，**`<transition-group>` 不再默认渲染根节点**。

- 如果像上面的示例一样，已经在 Vue 2 代码中定义了 `tag` attribute，那么一切都会和之前一样
- 如果没有定义 `tag` attribute，_而且_样式或其它行为依赖于 `<span>` 根元素的存在才能正常工作，那么只需将 `tag="span"` 添加到 `<transition-group>`：

``` vue
<transition-group tag="span">
  <!-- -->
</transition-group>
```

---

#### Watch 侦听数组
- 当侦听一个数组时，只有当数组被替换时才会触发回调。如果你需要在数组被改变时触发回调，必须指定 `deep` 选项。