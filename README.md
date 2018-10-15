## 安装开发环境
* 下载[VS Code](https://code.visualstudio.com/download) IDE，建议安装以下插件：
  * [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) 
  * [GraphQL for VSCode](https://marketplace.visualstudio.com/items?itemName=kumar-harsh.graphql-for-vscode)
  * [Sublime Babel](https://marketplace.visualstudio.com/items?itemName=joshpeng.sublime-babel-vscode)
  * [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
* 下载[NodeJS](https://nodejs.org/en/download/)
* 下载[Mongodb](https://www.mongodb.com/download-center?initial=true#atlas)并[安装](https://docs.mongodb.com/guides/server/install/)
* 安装Chrome的[React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)扩展程序

## 使用npm
* 基本概念
  * [package.json](https://docs.npmjs.com/files/package.json)记录项目依赖的包
  * `package-lock.json`由npm自动生成，记录node_modules和`package.json`的变更
  * `dependencies`记录运行时需要的包
  * `devDependencies`记录开发时需要的包
  * `scripts`记录`npm`可运行的命令
* 常用命令 
  * 安装`package.json`中所有的包
  ```
  npm install
  ```
  * 安装全局包 `-g`，如：
  ```
  npm typescript -g
  ```
  * 安装本项目运行时包 `--save`，如：
  ```
  npm react --save
  ```
  * 安装本项目开发时包 `--save-dev`，如：
  ```
  npm tslint --save-dev
  ```
  * 删除包，如：
  ```
  npm uninstall react --save
  ```
  * 查看可升级包
  ```
  npm outdated
  ```
  * 升级包，如：
  ```
  npm update tslint
  ```
  * 查看全局包
  ```
  npm list -g --depth 0
  ```
  * 查看包的版本信息，如：
  ```
  npm show react versions
  ```
  * 运行`scripts`命令，如：
  ```
  npm run storybook
  ```
  * 查看帮助信息
  ```
  npm help
  ```

## 配置TypeScript编译选项
* [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)中配置
* 一般地，`strictNullChecks`等均配置为true，以进行更严格的编译期检查

## 配置TSLint选项
* [tslint.config](https://palantir.github.io/tslint/rules/)中配置
* 一般地，尽量使用更严格的规则，偶尔有特殊情况使用[注释标记](https://palantir.github.io/tslint/usage/rule-flags/)制定忽略的规则

## 安装和配置React

### 创建项目

* 全局安装[Create React App](https://github.com/facebook/create-react-app)
    ```sh
    npm i -g create-react-app 
    ```

* 使用`create-react-app`创建TypeScript 项目并引入 [antd](https://ant.design/index-cn)
    ```sh
    create-react-app my-project --scripts-version=react-scripts-ts-antd 
    ```

* 运行项目
    ```sh
    npm start
    ```

### 安装Apollo

* 基本概念
  * [Apollo](https://www.apollographql.com/)是基于[GraphQL](https://graphql.org/)规范的工具库
  * [Apollo Client](https://www.apollographql.com/docs/react/)用于使用GraphQL构建客户端程序
  * React Apollo是Apollo Client和React的集成，用于从GraphQL服务器获取数据，在React框架中方便地构建用户界面
  
* [安装Apollo Client](https://github.com/apollographql/apollo-client)
    ```sh
    npm i --save apollo-boost graphql apollo-client apollo-cache-inmemory apollo-link apollo-link-http apollo-link-ws subscriptions-transport-ws @types/graphql @types/ws
    ```

* 安装[React Apollo](https://github.com/apollographql/react-apollo)
    ```sh
    npm i --save react-apollo
    ```

### 安装Immer

* [Immer](https://github.com/mweststrate/immer)用于方便地修改不可变的状态(immutable state)，一般地用于`React.Component`的`setState`方法
    ```sh
    npm i --save immer
    ```

### 安装recompose

* [recompose](https://github.com/acdlite/recompose)是用于React组件和高阶组件(higher-order components)的工具库。
    ```sh
    npm i --save recompose
    npm i -D @types/recompose
    ```

### 安装Enzyme
* 基本概念
  * [Enzyme](https://github.com/airbnb/enzyme)是React组件测试库
  * [Jest](https://github.com/facebook/jest)是测试运行框架，已由`create-react-app`安装
    ```sh
    npm i -D enzyme enzyme-adapter-react-16 @types/enzyme @types/enzyme-adapter-react-16
    ```
* 配置
    * 新增`src/jest.setup.ts`初始化Enzyme测试环境
    * `package.json`中配置`jest.setupTestFrameworkScriptFile`指向该文件

### 安装Storybook

* 基本概念
  * [Storybook](https://github.com/storybooks/storybook/tree/release/3.4)是React组件库开发环境，用于浏览、开发和测试组件库
  * [StoryShots](https://github.com/storybooks/storybook/tree/master/addons/storyshots/storyshots-core)利用Storybook自动进行Jest Snapshot测试
  * [jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot)利用对比截图进行视觉回归测试
  
* 安装Storybook
    ```sh
    npm i -g @storybook/cli
    cd my-react-app
    getstorybook
    ```

* 安装[TypeScript支持](https://storybook.js.org/configurations/typescript-config/)
    ```sh
    npm i -D awesome-typescript-loader @storybook/addon-info react-docgen-typescript-webpack-plugin @types/storybook__addon-actions @types/storybook__addon-links @types/storybook__addon-info @types/storybook__react
    ```
* 配置
  * 新增`.storybook/webpack.config.js`
  * 修改`.storybook/config.js`支持.ts和.tsx
  * `@storybook/react`升级为4.0.0-alpha.24，以匹配`StoryShots`的版本
  * `stories/index.stories.js`改名为`stories/index.stories.tsx`并修改import
  * 修改`tsconfig.json`

* 运行Storybook
    ```sh
    npm start storybook
    ```
  
* 浏览器中打开`http://localhost:6006/`

### 安装StoryShots
* 安装
    ```sh
    npm i -D @storybook/addon-storyshots@4.0.0-alpha.24  @types/storybook__addon-storyshots react-test-renderer
    ```

* 配置
  * `.storybook/config.js`中增加Jest下的`require.context`模拟实现

### 安装jest-image-snapshot
* 安装
    ```sh
    npm i -D jest-image-snapshot @types/jest-image-snapshot
    ```
* 配置
  * 在`src/jest.setup.ts`增加`toMatchImageSnapshot`
  * TODO 如何截图?
