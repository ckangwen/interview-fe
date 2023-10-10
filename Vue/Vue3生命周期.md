#Vue 


![[be25db0ffeae4655ae044d2dcf10e7f7~tplv-k3u1fbpfcp-zoom-in-crop-mark_1512_0_0_0.webp]]

beforeCreate
在实例初始化之后、数据观测(initState)和 event/watcher 事件配置之前被调用。
对于此时做的事情，如注册组件使用到的store或者service等单例的全局物件。
相比Vue2没有变化。

created
一个新的 Vue 实例被创建后（包括组件实例），立即调用此函数。
在这里做一下初始的数据处理、异步请求等操作，当组件完成创建时就能展示这些数据。
相比Vue2没有变化。

beforeMount
在挂载之前调用，相关的render函数首次被调用,在这里可以访问根节点，在执行mounted钩子前，dom渲染成功，相对Vue2改动不明显。

onMounted
在挂载后调用，也就是所有相关的DOM都已入图，有了相关的DOM环境，可以在这里执行节点的DOM操作。
在这之前执行beforeUpdate。

beforeUpdate
在数据更新时同时在虚拟DOM重新渲染和打补丁之前调用。
我们可以在这里访问先前的状态和dom，如果我们想要在更新之前保存状态的快照，这个钩子非常有用。
相比Vue2改动不明显。

onUpdated
在数据更新完毕后，虚拟DOM重新渲染和打补丁也完成了，DOM已经更新完毕。
这个钩子函数调用时，组件DOM已经被更新，可以执行操作，触发组件动画等操作

beforeUnmount
在卸载组件之前调用。在这里执行清除操作，如清除定时器、解绑全局事件等。

onUnmounted
在卸载组件之后调用，调用时，组件的DOM结构已经被拆卸，可以释放组件用过的资源等操作。

onActivated
被 `keep-alive` 缓存的组件激活时调用。

onDeactivated
被 `keep-alive` 缓存的组件停用时调用。

onErrorCaptured
当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。
此钩子可以返回 `false` 以阻止该错误继续向上传播。



beforeDestroy改名为 beforeUnmount
destroyed改名为 unmounted


beforeCreate ===> setup()
created      ===> setup()
beforeMount  ===> onBeforeMount
mounted      ===> onMounted
beforeUpdate ===> onBeforeUpdate
updated      ===> onUpdated
beforeUnmount===> onBeforeUnmount
unmounted    ===> onUnmounted

  
  
作者：EazerCode  
链接：https://www.jianshu.com/p/4397a7d08971  
来源：简书  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。