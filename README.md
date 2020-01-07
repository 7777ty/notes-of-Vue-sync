# Vue中.sync修饰符的二三事

**.sync修饰符的历史**


> 原先.sync修饰符存在于Vue的1.0版本中，但是在2.0中被官方移除了。然而在Vue2.0发布后的实际应用中，人们发现在开发可复用的组件库时，.sync修饰符还是有用武之地的，于是在Vue2.3.0版本中，又重新引入了这一修饰符。这次它成了一个语法糖。


这里引用官方文档中的一个例子,在一个包含 title prop 的假设的组件中，我们可以用以下方法表达对其赋新值的意图：

```JS
this.$emit('update:title', newTitle)
```

然后父组件可以监听那个事件并根据需要更新一个本地的数据属性。例如：

```JS
<text-document
  v-bind:title="doc.title"
  v-on:update:title="doc.title = $event"
></text-document>
```

为了方便起见，Vue为这种模式提供一个缩写，即 .sync 修饰符：

```JS
<text-document v-bind:title.sync="doc.title"></text-document>
```

即代码```<text-document v-bind:title.sync="doc.title"></text-document>```会被扩展成```<text-document v-bind:title="doc.title" v-on:update:title="doc.title = $event"></text-document>```，说明了.sync修饰符就是一个语法糖，它的作用与它拓展后的代码相同：当一个子组件改变了一个 prop 的值时，这个变化也会同步到父组件中所绑定。
