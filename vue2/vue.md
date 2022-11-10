组件代码顺序(☆☆☆☆)
组件中的生命周期函数按照生命周期的顺序来敲代码，

```
beforeCreate-->created-->beforeMount-->mounted-->beforeUpdate-->updated-->beforeDestroy-->destroyed
```

样式代码顺序(☆☆☆☆)

- Formatting Model 相关属性包括：position / top / right / bottom / left / float / display / overflow 等
- Box Model 相关属性包括：border / margin / padding / width / height 等
- Typographic 相关属性包括：font / line-height / text-align / word-wrap 等
- Visual 相关属性包括：background / color / transition / list-style 等

- 避免使用过多的 if else,可以使用简单逻辑 switch

组件命名规范（☆）

- 基础组件使用 base 开头，业务组件使用 custom 开头，
- 为了区别组件可以根据情形使用 global，common，\_ 等开头

````
compoents
   MyButton.vue // vue 后缀，首字母大写+驼峰
   base-comps
       base-button
           base-button.ts
```


路由命名规范（☆☆☆☆☆）

- 路由命名采用全小写，单词用 - 隔开格式 因为如果你使用下划线或者驼峰形式，会被当成一个单词，搜索引擎无法区分语义

``` const routes: Array<RouteConfig> = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about-us', // 使用 - 隔开，会被解析为 about 和 us  搜索引擎更容易识别
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]
````

#### 事件，方法命名规范(☆☆☆☆☆)

$emit 事件名一般用 on-eventName

自定义方法分为很多种，一般使用 handle 前缀,如果是一歇判断方法，包含方法，获取值，设置值等，则分别有自己的前缀，采用前缀+事件名，小驼峰命名形式
handle 大部分自定义方法前缀
has 是否包含某值方法前缀
is 是否为某个值
get 获取某值
set 设置某值

#### 变量，常量命名规范方式(☆☆☆☆☆)

- 变量一般使用 let 来声明，驼峰命名格式，语义化
- 常量使用 const 雷生命，是用大写字母，用下划线隔开
- 尽量避免使用 var 定义变量

```
let homeTitle: string = "首页标题" //变量
const MAX_SCREEN_VALUE：number = 1920//常量
```

- prop 的定义应该尽量详细，有以下两处优点：他们呢写明了组件的 api，所以容易看懂组件的用法，在开发环境下，如果一个组件提供格式不争的 prop，Vue 将会警告，以辅助捕获前在的错误来源

- 组件上总是必须 key 配合 v-for，以便维护内部组件及其子树的状态
- 避免 v-if 和 v-for 用在一起，因为 v-for 比 v-if 具有更高的优先级

- 单文件组件的文件名应该以大写字母开头

- 为非公有组件样式设置作用域(scoped 属性运用),防止样式相互之间影响

- 在单文件组件和字符串模板中组件名应该总是大写字母开头(DoctorAccount)，在 template 模板使用组件时，使用 kebab-case(短横线链接 doctor-account)

#### 组件/实例的选项顺序(逐渐形成顺序)

```
name
components / directives / filters
extends / mixins
model / props / propsData
data / computed
watch / 生命周期钩子
methods
```

代码样例

```
<script>
  export default {
    name: 'ExampleName',  // 这个名字推荐：大写字母开头驼峰法命名。
    props: {},            // Props 定义。
    components: {},       // 组件定义。
    directives: {},       // 指令定义。
    mixins: [],           // 混入 Mixin 定义。
    data () {              // Data 定义。
      return {
        dataProps: ''     // Data 属性的每一个变量都需要在后面写注释说明用途
      }
    },
    computed: {},         // 计算属性定义。
    created () {},         // 生命钩子函数，按照他们调用的顺序。
    mounted () {},         // 挂载到元素。
    activated () {},       // 使用 keep-alive 包裹的组件激活触发的钩子函数。
    deactivated () {},     // 使用 keep-alive 包裹的组件离开时触发的钩子函数。
    watch: {},            // 属性变化监听器。
    methods: {            // 组件方法定义。
      publicbFunction () {}  // 公共方法的定义，可以提供外面使用
      _privateFunction () {} // 私有方法，下划线定义，仅供组件内使用。
    }
  }
</script>
```

#### 元素特性的顺序(逐渐形成习惯)

```
is
v-for / v-if / v-else-if / v-else / v-show / v-cloak
v-pre / v-once
id
ref / key / slot
v-model
v-on
v-html / v-text
```

#### 事件的控制

- 尽量避免使用 this.parent、thi.root 进行控制，会导致流程难以追踪，可使用事件中心进行代替。
- 组件当中有原生绑定事件，组件注销前移除。

坚持一致性的原则，一个团队的代码风格如果统一了，能够培养良好的协同和编码习惯，提高代码的质量和可维护性
