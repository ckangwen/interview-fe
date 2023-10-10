#Vue

> https://juejin.cn/post/6844904050014552072

```ts
// 需要定义响应式的原值
export type Raw = object
// 定义成响应式后的proxy
export type ReactiveProxy = object

// 用来存储原始值和响应式proxy的映射
export const proxyToRaw = new WeakMap<ReactiveProxy, Raw>()
// 用来存储响应式proxy和原始值的映射
export const rawToProxy = new WeakMap<Raw, ReactiveProxy>()

function createReactive<T extends Raw>(raw: T): T {
  // 在 baseHandlers 建立对 get、set的劫持
  const reactive = new Proxy(raw, baseHandlers)

  // 双向存储原始值和响应式proxy的映射
  // 后续无论是拿到原始对象还是拿到响应式proxy，都可以很容易的拿到它们的另一半
  rawToProxy.set(raw, reactive)
  proxyToRaw.set(reactive, raw)

  // 建立一个映射
  // 原始值 -> 存储这个原始值的各个key收集到的依赖函数的Map
  storeObservable(raw)

  // 返回响应式proxy
  return reactive as T
}
```

**storeObservable**
```ts
// 收集响应依赖的的函数
export type ReactionFunction = Function & {
  cleaners?: ReactionForKey[]
  unobserved?: boolean
}

// reactionForRaw的key为对象key值 value为这个key值收集到的Reaction集合
export type ReactionForRaw = Map<Key, ReactionForKey>

// key值收集到的Reaction集合
export type ReactionForKey = Set<ReactionFunction>

// 收集响应依赖的的函数
export type ReactionFunction = Function & {
  cleaners?: ReactionForKey[]
  unobserved?: boolean
}


const connectionStore = new WeakMap<Raw, ReactionForRaw>()

function storeObservable(value: object) {
  // 存储对象和它内部的key -> reaction的映射
  // 原始数据 -> 这个数据收集到的观察函数依赖
  connectionStore.set(value, new Map() as ReactionForRaw)
}

```

**proxy 的handler**

``` ts
/** 劫持get访问 收集依赖 */
function get(target: Raw, key: Key, receiver: ReactiveProxy) {
  const result = Reflect.get(target, key, receiver)
  
  // 收集依赖
  registerRunningReaction({ target, key, receiver, type: "get" })

  return result
}

```

**get 收集依赖**

```ts
// 收集响应依赖的的函数
type ReactionFunction = Function & {
  cleaners?: ReactionForKey[]
  unobserved?: boolean
}

// 操作符 用来做依赖收集和触发依赖更新
interface Operation {
  type: "get" | "iterate" | "add" | "set" | "delete" | "clear"
  target: object
  key?: Key
  receiver?: any
  value?: any
  oldValue?: any
}

/** 依赖收集栈 */
const reactionStack: ReactionFunction[] = []

/** 依赖收集 在get操作的时候要调用 */
export function registerRunningReaction(operation: Operation) {
  const runningReaction = getRunningReaction()
  if (runningReaction) {
      // 拿到原始对象 -> 观察者的map
      const reactionsForRaw = connectionStore.get(target)
      // 拿到key -> 观察者的set
      let reactionsForKey = reactionsForRaw.get(key)
    
      if (!reactionsForKey) {
        // 如果这个key之前没有收集过观察函数 就新建一个
        reactionsForKey = new Set()
        // set到整个value的存储里去
        reactionsForRaw.set(key, reactionsForKey)
      }
    
      if (!reactionsForKey.has(reaction)) {
        // 把这个key对应的观察函数收集起来
        reactionsForKey.add(reaction)
        // 把key收集的观察函数集合 加到cleaners队列中 便于后续取消观察
        reaction.cleaners.push(reactionsForKey)
      }
  }
}

/** 从栈的末尾取到正在运行的observe包裹的函数 */
function getRunningReaction() {
  const [runningReaction] = reactionStack.slice(-1)
  return runningReaction
}

```

