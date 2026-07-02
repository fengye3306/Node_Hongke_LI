
## Markdown 使用备忘

本仓库用 [docsify](https://docsify.js.org) 渲染。除标准 Markdown 外，docsify 扩展了一批语法；数学公式通过 `docsify-latex` + MathJax 3 支持标准 LaTeX 分隔符（`$...$`、`$$...$$`、`\(...\)`、`\[...\]`）。

---

## 通用 Markdown

### 标题与强调

```markdown
## 二级标题
### 三级标题

**粗体**  *斜体*  `行内代码`
```

### 代码块

````markdown
```shell
.\vcpkg install duckdb:x64-windows
```
````

### 链接与图片

```markdown
[文字](./path/to/page.md)
![说明](https://example.com/image.png)
```

### 列表

```markdown
- 无序项
  - 子项

1. 有序项
```

### 数学公式（LaTeX）

本站通过 `docsify-latex` + MathJax 3 渲染，分隔符与常见 Markdown + LaTeX 写法一致（Pandoc / GitHub / Typora 同类习惯）。

| 类型 | 写法 | 示例 |
|------|------|------|
| 行内公式 | `$...$` 或 `\(...\)` | `$e^{i\theta}$` |
| 独立公式 | `$$...$$` 或 `\[...\]` | 见下方欧拉公式块 |

**行内示例：**

```markdown
乘以 $e^{i\theta}$，就是旋转 $\theta$。
```

乘以 $e^{i\theta}$，就是旋转 $\theta$。

也可用 LaTeX 标准括号：

```markdown
欧拉恒等式 \(e^{i\pi}+1=0\) 将五个常数联系在一起。
```

**独立一行（块级）示例：**

```markdown
$$
e^{i\theta} = \cos\theta + i\sin\theta
$$
```

$$
e^{i\theta} = \cos\theta + i\sin\theta
$$

**欧拉公式备忘（可直接复制）：**

```markdown
## 欧拉公式

欧拉公式：

$$
e^{i\theta} = \cos\theta + i\sin\theta
$$

令 $\theta = \pi$，得欧拉恒等式：

$$
e^{i\pi} + 1 = 0
$$

几何意义：复数乘以 $e^{i\theta}$，相当于在复平面上逆时针旋转 $\theta$（弧度）。
```

**常用符号：**

```markdown
$\alpha,\beta,\theta$          % 希腊字母
$x^2,\,e^{i\theta}$            % 上下标
$\frac{a}{b},\,\sqrt{x}$        % 分式、根号
$\sum_{i=1}^{n} x_i$            % 求和
$\int_a^b f(x)\,dx$             % 积分
```

**注意：**

- 行内公式前后留空格，避免和相邻 `$` 粘连。
- 美元符号作货币时写 `\$100`。
- 块级公式 `$$` 单独占行，上下各空一行更稳妥。
- 配置见根目录 `index.html` 的 `latex` 项；已移除非标准的 `@` / `@@` 分隔符。

### 引用

```markdown
> 引用内容
```

---

## docsify 文档助手

### 强调内容（重要提示）

语法：`!> 内容`

```markdown
!> 一段重要的内容，可以和其他 **Markdown** 语法混用。
```

### 普通提示

语法：`?> 内容`

```markdown
?> _TODO_ 完善示例
```

### 忽略编译链接

默认 `[link](/demo/)` 会被 docsify 编译为 SPA 路由。若要跳转到真实路径：

```markdown
[link](/demo/ ':ignore')
[link](/demo/ ':ignore title')
```

### 链接属性

```markdown
[新窗口打开](/demo ':target=_blank')
[当前窗口](/demo2 ':target=_self')
[禁用](/demo ':disabled')
```

跨域链接（`routerMode: 'history'` 且 `externalLinkTarget: '_self'` 时需加）：

```markdown
[example.com](https://example.com/ ':crossorgin')
```

### GitHub 任务列表

```markdown
- [ ] 未完成
- [x] 已完成
  - [ ] 子任务
```

注意：`- [] bam` 无效，方括号内必须有空格。

### 图片处理

```markdown
![logo](url ':size=50x100')
![logo](url ':size=100')
![logo](url ':size=10%')
![logo](url ':class=someCssClass')
![logo](url ':id=someCssId')
```

### 标题 id

```markdown
### 你好，世界！ :id=hello-world
```

锚点：`#/page?id=hello-world`

### HTML 标签中的 Markdown

HTML 与 Markdown 内容之间需**空一行**：

```markdown
<details>
<summary>自我评价（点击展开）</summary>

- 项目 A
- 项目 B

</details>
```

```markdown
<div style='color: red'>

- listitem
- listitem

</div>
```

---

## docsify 兼容 Vue

在 Markdown 里可直接写 Vue 模板，页面加载时执行。需先在 `index.html` 引入 Vue：

```html
<!-- Vue 3 生产版 -->
<script src="//cdn.jsdelivr.net/npm/vue@3/dist/vue.global.prod.js"></script>
```

本站当前 `executeScript: true`，但未引入 Vue；要用下列功能需自行添加脚本。

### 模板语法

```html
<p v-if="false">仅在 GitHub 等纯 Markdown 环境显示</p>

<ul>
  <li v-for="i in 3">Item {{ i }}</li>
</ul>

<p>2 + 2 = {{ 2 + 2 }}</p>
```

配合 `data` / `computed` / `methods`：

```html
{{ message }}

<p v-text="message"></p>

<button @click="hello">Say Hello</button>
```

### 配置方式（`window.$docsify`）

| 选项 | 作用 |
|------|------|
| `vueGlobalOptions` | 全局 Vue 选项；data 跨页面持久、实例间共享 |
| `vueMounts` | 按 CSS 选择器挂载；每实例 data 独立，换页不保留 |
| `vueComponents` | 注册全局组件；每实例 data 独立 |

```javascript
window.$docsify = {
  vueGlobalOptions: {
    data() {
      return { count: 0 };
    },
  },
  vueMounts: {
    '#counter': {
      data() {
        return { count: 0 };
      },
    },
  },
  vueComponents: {
    'button-counter': {
      template: `<button @click="count += 1">clicked {{ count }}</button>`,
      data() { return { count: 0 }; },
    },
  },
};
```

### Markdown 内 `<script>` 挂载

仅**第一个** `<script>` 标签会执行；多实例须写在同一脚本内。

```html
<!-- Vue 3 -->
<script>
  Vue.createApp({
    data() { return { message: 'Hello' }; },
  }).mount('#example');
</script>
```

### 处理顺序（每次加载页面）

1. 执行 Markdown `<script>`
2. 注册 `vueComponents`
3. 挂载 `vueMounts`
4. 自动挂载未挂载的 `vueComponents`
5. 用 `vueGlobalOptions` 自动挂载含模板语法的顶级元素

含 `{{ }}` 或组件的**顶级** HTML 元素会被自动挂载；已存在 Vue 实例的节点不会重复挂载；换页前 docsify 会销毁它创建的实例。

---

## 常用 docsify 页面指令

```markdown
<!-- {docsify-ignore} -->        <!-- 侧边栏忽略本标题 -->
<!-- {docsify-ignore-all} -->    <!-- 本页标题均不进侧边栏 -->
```

`node/read/README.md` 已使用 `{docsify-ignore-all}`。
