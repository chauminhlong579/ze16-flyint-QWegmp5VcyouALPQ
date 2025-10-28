## import('../views/Login.vue'), 提示找不到模块或其相应的类型声明；

**技术栈：ts+vue3+vite**

### 创建一个 **vite-env.d.ts**文件

`///`

`declare module '*.vue' {`
`import type { DefineComponent } from 'vue'`
`const component: DefineComponent<{}, {}, any>`
`export default component`
`}`

---

上面代码用于在 TypeScript 项目中为 .vue 文件提供类型支持

### 在 TypeScript 中，三斜线指令是一种特殊的注释，用于告诉编译器在编译时包含额外的类型定义文件。

`///`  表明当前项目依赖于 vite/client 这个类型定义包。

* 这是一个 TypeScript 三斜线指令（triple-slash directive）
* 它告诉 TypeScript 编译器引入 Vite 客户端的类型声明
* 这样就能获得 Vite 提供的内置类型支持，如导入静态资源（图片、CSS 等）时的类型提示

`vite/client` 是 Vite 框架提供的类型定义文件，它包含了 Vite 客户端相关的类型信息，比如环境变量类型、导入模块的类型等。通过引入这个类型定义，TypeScript 编译器就能正确识别和处理与 Vite 客户端相关的代码。

### `declare module` 是在 TypeScript 中声明一个模块的语法

`declare module '*.vue'`

* 这是 TypeScript 的模块声明语法，用于为没有类型定义的模块提供类型声明
* 具体来说，它为所有 .vue 文件扩展名的模块声明了类型
* 在 TypeScript 中，默认不认识 .vue 文件，所以需要这个声明

### 从 Vue 中导入 `DefineComponent` 类型

`import type { DefineComponent } from 'vue'`

* 从 Vue 中导入 DefineComponent 类型
* 使用 import type 表示只导入类型，不会在运行时引入实际代码

### 声明一个名为 component 的常量，类型为 DefineComponent

`const component: DefineComponent<{}, {}, any>`

* 声明一个名为 component 的常量，类型为 DefineComponent
* DefineComponent 是 Vue 组件的类型，有三个泛型参数：
  -- 第一个 {} 表示组件的 props 类型为空对象
  -- 第二个 {} 表示组件的 emits 类型为空对象
  -- 第三个 any 表示组件的插槽内容类型为 any（任意类型）

### 将 `component` 作为默认导出

`export default component`

* 将 component 作为默认导出
* 这样在导入 .vue 文件时，TypeScript 就知道默认导出的是一个 Vue 组件
  **这段代码的主要作用是让 TypeScript 能够正确识别和处理 .vue 文件的导入，为 Vue 单文件组件提供类型支持。当你在代码中使用 import xxx from './xxx.vue' 时，TypeScript 编译器就会根据这个声明文件知道导入的是一个 Vue 组件，并提供相应的类型检查**

本博客参考[黑猫加速器](https://heimaojiasuqi.com)。转载请注明出处！
