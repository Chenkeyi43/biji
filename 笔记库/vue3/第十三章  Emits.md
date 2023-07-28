除了接收 props，子组件还可以向父组件触发事件：


``` vue
<script setup>
// 声明触发的事件
const emit = defineEmits(['response'])

// 带参数触发
emit('response', 'hello from child')
</script>
```

`emit()` 的第一个参数是事件的名称。其他所有参数都将传递给事件监听器。

父组件可以使用 `v-on` 监听子组件触发的事件——这里的处理函数接收了子组件触发事件时的额外参数并将它赋值给了本地状态：


``` html
<ChildComp @response="(msg) => childMsg = msg" />
```

现在在编辑器中自己尝试一下吧。
App.vue
``` vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const childMsg = ref('No child msg yet')
</script>

<template>
 <--父组件可以使用 `v-on` 监听子组件触发的事件-->
  <ChildComp @response="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>
</template>

```
childcomp.vue
```vue
<script setup>
  // 声明触发的事件
const emit = defineEmits(['response'])
// 带参数触发
emit('response', 'hello from child')
</script>

<template>
  <h2>Child component</h2>
</template>
```