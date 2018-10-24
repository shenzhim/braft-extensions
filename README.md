# Braft Editor扩展模块包

### 目前包含的模块列表
1. 代码高亮模块 CodeHighlighter
2. 高级取色器模块 ColorPicker
3. 表情包扩展模块 Emoticon

### 安装
```bash
npm install braft-extensions --save
# 或者
yarn add braft-extensions
```

### 使用
需要分别import本模块包下面的各个模块，参见下方各模块的基本使用介绍

## 代码高亮模块
使用[prismjs](https://github.com/PrismJS/prism)和[draft-js-prism](https://github.com/SamyPesse/draft-js-prism)开发的一个代码高亮模块，能在编辑器中实现代码高亮编辑功能，内置html、js和css语言支持，可扩展更多语言，[在线演示](https://braft.margox.cn/demos/code-highlighter)

#### 安装依赖
```bash
npm install prismjs draft-js-prism --save
# 或者
yarn add prismjs draft-js-prism
```

#### 基本使用
```js
import 'braft-editor/dist/index.css'
import 'braft-extensions/dist/code-highlighter.css'

import BraftEditor from 'braft-editor'
import CodeHighlighter from 'braft-extensions/dist/code-highlighter'

const options = {
  includeEditors: ['editor-id-1'], // 指定该模块对哪些BraftEditor生效，不传此属性则对所有BraftEditor有效
  excludeEditors: ['editor-id-2']  // 指定该模块对哪些BraftEditor无效
}

BraftEditor.use(CodeHighlighter(options))
```

#### 扩展语言支持
请访问[PrismJs官网](https://prismjs.com/#languages-list)查看全部支持的语言
```js
// 首先需要从prismjs中引入需要扩展的语言库
import 'prismjs/components/prism-java'
import 'prismjs/components/prism-php'

// 通过opitons.
const options = {
  syntaxs: [
    {
      name: 'JavaScript',
      syntax: 'javascript'
    }, {
      name: 'HTML',
      syntax: 'html'
    }, {
      name: 'CSS',
      syntax: 'css'
    }, {
      name: 'Java',
      syntax: 'java',
    }, {
      name: 'PHP',
      syntax: 'php'
    }
  ]
}

BraftEditor.use(CodeHighlighter(options))
```

#### 使用其他Prism配色主题
该功能将在后续版本中支持

#### 使用注意事项
- 使用该模块，必须引入braft-extensions/dist/code-highlighter.css文件
- 该模块仅用于对编辑器内的代码块进行高亮展示，并不会更改编辑器输出的实际内容，如果需要在展示页面进行代码高亮，请单独使用Prism.js或其他代码高亮方案进行处理


## 高级取色器模块
使用[react-color](https://github.com/casesandberg/react-color)来替换编辑器自身的颜色选择模块，设置颜色更自由！[在线演示](https://braft.margox.cn/demos/color-picker)

#### 安装依赖
```bash
npm install react-color --save
# 或者
yarn add react-color
```

#### 基本使用
```js
import 'braft-editor/dist/index.css'
import 'braft-extensions/dist/color-picker.css'

import BraftEditor from 'braft-editor'
import ColorPicker from 'braft-extensions/dist/color-picker'

const options = {
  includeEditors: ['editor-id-1'], // 指定该模块对哪些BraftEditor生效，不传此属性则对所有BraftEditor有效
  excludeEditors: ['editor-id-2'],  // 指定该模块对哪些BraftEditor无效
  theme: 'light', // 指定取色器样式主题，支持dark和light两种样式
}

BraftEditor.use(ColorPicker(options))
```

#### 使用注意事项
- 使用该模块，必须引入braft-extensions/dist/color-picker.css文件


## 表情包扩展模块
替换内置的emoji组件，可以插入图片形式的表情，[在线演示](https://braft.margox.cn/demos/emoticon)

#### 基本使用
```js
import 'braft-editor/dist/index.css'
import BraftEditor from 'braft-editor'

// 引入表情包扩展模块样式文件
import 'braft-extensions/dist/emoticon.css'
// 引入表情包扩展模块和默认表情包列表
import Emoticon, { defaultEmoticons } from 'braft-extensions/dist/emoticon'

// 转换默认表情包列表，让webpack可以正确加载到默认表情包中的图片，请确保已对png格式的文件配置了loader
// 如果你使用的webpack版本不支持动态require，或者使用的其他打包工具，请勿使用此写法
const emoticons = defaultEmoticons.map(item => require(`braft-extensions/dist/assets/${item}`))

// 也可以使用自己的表情包资源，不受打包工具限制
// const emoticons = ['http://path/to/emoticon-1.png', 'http://path/to/emoticon-2.png', 'http://path/to/emoticon-3.png', 'http://path/to/emoticon-4.png', ...]

const options = {
  includeEditors: ['editor-id-1'], // 指定该模块对哪些BraftEditor生效，不传此属性则对所有BraftEditor有效
  excludeEditors: ['editor-id-2'],  // 指定该模块对哪些BraftEditor无效
  emoticons: emoticons, // 指定可用表情图片列表，默认为空
}

BraftEditor.use(Emoticon(options))
```

#### 默认表情包来自https://www.iconfinder.com/iconsets/emoji-18 [[CC BY 3.0](https://creativecommons.org/licenses/by/3.0/#)]，由[Bukeicon](https://www.iconfinder.com/bukeicon)创建

#### 使用注意事项
- 使用该模块，必须引入braft-extensions/dist/emoticon.css文件