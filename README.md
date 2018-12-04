# APICloud Kit

## 前言

- [APICloud](http://www.apicloud.com) 是一个 xxxx 的工具，我们用 APICloud 一个月上线了一个项目。
- APICloud 是一个用 web 技术写原生 APP 的工具
- Js 接口封装不太友好
- 官方仍然建议使用 jQuery + 模版引擎的方式开发，显得有点点与主流 web 技术脱节
- 没有 d.ts，不兼容 [TypeScript](http://www.typescriptlang.org)
- 于是打算开发一套 APICloud 全家桶，用于快速开发 APICloud 项目
- 代码还没写一句，决定这次先写文档
- 以下是对该项目的一个规划，看看就好

## 目录

- [cli](#cli)

  - 根据[project.config.ts](#projectconfigts) 读取生成项目[目录结构](#目录结构)
  - 可监听 project.config.ts 变化

- [运行时](#运行时)

  - 书写 APICloud api 对象接口的 d.ts
  - promisify 封装 api 对象接口
  - 路由封装
  - frame 封装
  - 运行时可更新
    `

- [工具](./docs/Tools.md)

  - 远程 devtool 工具
  - 错误监控工具
  - 开发工具包

- [项目模版](#template)

  - Preact
  - React
  - Vue
  - jQuery + 模版引擎
  - 原生 `document.queryselector()` + 模版引擎

## cli

#### project.config.ts

代码片段

```typescript
interface Config {
  pages: {
    name: string;
    frames: {
      name: string;
      data: any;
      headers: any;
      url: string;
      rect?: {
        x?: number;
        y?: number;
        w?: number | 'auto';
        h?: number | 'auto';
      };
      // ... 省略`api.openFrame()` 更多参数]
    }[];
  }[];
}

export const config: Config = {
  pages: [
    {
      name: 'root',
      frames: [
        {
          name: 'firstFrame',
          url: ''
        }
      ]
    }
  ]
};
```

文档

[api.openFrame](https://docs.apicloud.com/Client-API/api#27)

#### 目录结构

```bash
| -- src
    | -- pages
        | -- Root.tsx
    | -- frames
        | -- FrameOne.tsx
        | -- FrameTwo.tsx
    | -- styles
        | -- common.scss
        | -- color-vars.scss
    | -- App.tsx
    | -- config.ts
    | -- types
        | -- common.d.ts
| -- test
| -- dist
| -- project.config.ts
| -- .prettierrc
| -- tslint.js
| -- tsconfig.json
| -- package.json
| -- package-lock.json
| -- config.xml

```

## 运行时
