# 👨‍💻 React 编码约定

良好的代码规范能够提高代码的可读性，便于 `写作`、`沟通`、`PR Reivew`、减少 `bug`的出现等等，而 `React Coding Conventions` 主要围绕了这几点进行 `React`、`React Native` 的编码约定，统一编码规范，让代码看的更加赏心悦目。

# 状态管理和样式系统

为了减少开发资源之间的学习成本，尽量使用以下建议的状态管理和样式系统，如有添加应该提议题在委员会会议上讨论。

#### 状态管理

- mobx state tree
- recoil
- hox

#### 样式系统

- css in js
- css module
- sass
- less
- tailwindcss

# 命名约定

#### 文件、目录命名

文件、目录命名必须以烤串 **（kebab-case）** 命名，例如：`axios-logger`、`home-screen.tsx`、`api-config.ts`

#### 组件

```tsx
// React 组件必须以大驼峰（CamelCase）命名
const BaseButton = () => {...}

// 组件建议使用 interface 声明 props，并且使用 IxxxProps 方式命名
interface IModalProps {...}

const Modal = (props: IModalProps) => {...}

// 组件回调属性建议使用 onXXX 命名
interface IModalProps {
  onClose: () => void;
}

// 组件内处理回调属性函数建议使用 handleXXX 命名
const handleClose = () => {...}

<Modal onClose={handleClose} />
```

#### 变量

```tsx
// 变量必须以小驼峰（camelCase）命名
const userName = "Tom Lee";
```

#### 函数

```tsx
// 函数必须以小驼峰（camelCase）方式命名
const handleClick = () => {...}
```

#### Interface

```tsx
// Interface 必须 I 开头 + 大驼峰（CamelCase）方式命名，IXxx
interface IUser {
  id: number;
  name: string;
}
```

#### Type

```tsx
// Type 类型必须使用大驼峰（CamelCase）+ 结尾 Type 方式命名， XxxxType
type MethodType = "GET" | "POST" | "PUT" | "PATCH" | "DELETE";
```

#### Enum

```tsx
// Enum 枚举类型必须使用大驼峰（CamelCase）+ 结尾 Enum 方式命名， XxxxEnum
enum LoginTypeEnum {
  Password,
  VerifyCode,
}
```

# 目录结构

#### 总体结构

```
|- app
  |- components - 公共组件
  |- config - 环境配置文件
  |- hooks - 自定义钩子
  |- i18n - 多国语言翻译资源
  |- model - 状态管理文件
  |- navigation - 导航组件（仅限react native）
  |- routers - 路由组件（仅限react web）
  |- screens - 应用屏幕组件（仅限react native）
  |- pages - 应用页面组件（仅限react web）
  |- services - 外界连接服务
  |- theme - 应用主题、间距、颜色、排版
  |- types - 公共类型
  |- utils - 辅助工具

```

#### components

应用内可复用组件存放位置，一个目录对应一个组件，如出现组件比较庞大的情况，可拆分数个小组件存放在对应组件目录下，不需要建 `components` 目录。

```
|- app
  |- components
    |- base-button
      |- base-button.tsx
      |- base-button-text.tsx
      |- base-button-left.tsx
      |- base-button-right.tsx
```

#### hooks

应用内可复用 `hooks` 或者 `Context Providers`，例如 `use-loading`、`use-popup`、`use-confirm`、`use-keyboard-status`，简单的 `hooks` 可以创建一个文件存放，但是遇到比较复杂的 `hooks` 或者需要结合 `Context Provider` 使用的 `hooks`，需要创建对应目录，并且目录内放置 `index.tsx` 导出。

```
|- app
  |- hooks
    |- use-keyboard-status.ts
    |- use-confirm
      |- confirm-context.tsx
      |- confirm-dialog.tsx
      |- use-confirm.tsx
      |- index.tsx
```

#### screen and pages

应用的页面 **（屏幕）** 组件存放位置，一个页面 **（屏幕）** 组件对应一个目录，如出现页面 **（屏幕）** 比较庞大的情况，可在页面 **（屏幕）** 目录创建 `components` 目录，存放拆分的小组件，但是小组件不能继续有 `components` 目录，
如果页面 **（屏幕）** 组件逻辑比较多，可使用 `hooks` 拆分逻辑存放到页面（屏幕）目录下。

```
|- app
  |- pages
    |- home
      |- components
        |- header
          |- header.tsx
        |- footer
          |- footer.tsx
      |- home.tsx
      |- hooks.ts
```

####

#### services/api

建议 `api service` 根据 **模块拆分**，并且目录放置 `index.ts` 导出，避免随着功能迭代，单个文件代码超长，影响代码阅读性。

```
|- app
  |- services
    |-api
      |- api.ts
      |- api-auth.ts
      |- api-user.ts
      |- api-order.ts
      |- index.ts
```

# 代码规范

#### 不要使用默认导出

使用时需要命名，容易导致各个模块命名不一致。

```tsx
// Bad
const getUsers = () => {...};

export default getUsers;

// Good
export const getUsers = () => {...};
```

#### 使用 ES6 箭头函数

箭头函数允许我们使用更短的语法来编写函数。

```tsx
// Bad
function getUsers() {...};

// Good
const getUsers = () => {...};
```

#### 其他规范

其他规范已写在 ESLint 规则里面

react-native：[sj-distributor/eslint-plugin-react-native](https://github.com/sj-distributor/eslint-plugin-react-native)

react：待开发

# 关于注释

如何使用注释，其实一直是一个备受争议的话题，在 `《Clean Code》` 这本书说到好的代码是不需要注释的，但是我觉得毕竟现在 `99%` 的语言都是以英语表达为主，并非我们的母语，阅读起来并没有这么流畅，所以合适添加注释是很有必要的，特别我们都是开发业务系统多，适量的注释，对日后接手项目的同事会有一定的帮助。
