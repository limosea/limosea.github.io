---
title: "在React Native中使用Tailwind CSS"
tags: ["Android开发", "React Native"]
categories: ["Android开发"]
#externalUrl: ""
showSummary: true
date: 2026-01-28
draft: false
---

# 在React Native中使用Tailwind CSS

Tailwind CSS是一个用于构建用户界面的 CSS 框架，但该框架仅适用于Web端，在RN中，由于RD的设计模式，无法直接使用，需要一些折腾，本文介绍使用**NativeWind**来解决这个问题。

## 开始安装
NativeWind是一个用于React Native的Tailwind CSS工具，它可以将Tailwind CSS样式应用到React Native组件中，能让你像在React Web端那样使用className属性来定义样式。
> 如果你是新项目，或者刚开始的项目，那么我强烈建议你使用 [expo](https://docs.expo.dev/get-started/create-a-project/) 创建一个新项目，在expo中你可以回到熟悉的nextjs（基于文件目录的路由）。

### 创建项目
{{< tabs >}}
    {{< tab label="npm" >}}

    ```bash
        npx rn-new@next --nativewind
    ```
    {{< /tab >}}

    {{< tab label="yarn" >}}
    ```bash
        yarn dlx rn-new@next --nativewind
    ```
    {{< /tab >}}

    {{< tab label="pnpm" >}}
    ```bash
        pnpx rn-new@next --nativewind
    ```
    {{< /tab >}}

{{< /tabs >}}

> 如果你是老项目，需要安装并逐步配置
### 安装NativeWind
注意看[最新版本](https://www.nativewind.dev/docs/getting-started/installation#1-install-nativewind)，当前为NativeWind v5
<br/>
如果已安装[安装expo-cli](https://docs.expo.dev/more/expo-cli/#installation),尽量使用expo安装
{{< tabs >}}

    {{< tab label="expo" >}}

    ```bash
    npx expo install nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context
    ```
    {{< /tab >}}

    {{< tab label="npm" >}}
    ```bash
    npm install nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context
    ```
    {{< /tab >}}

    {{< tab label="yarn" >}}
    ```bash
    yarn add nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context
    ```
    {{< /tab >}}

    {{< tab label="pnpm" >}}
    ```bash
    pnpm install nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context
    ```
    {{< /tab >}}

{{< /tabs >}}

### 安装Tailwind CSS

{{< tabs >}}

    {{< tab label="expo" >}}

    ```bash
    npx expo install --dev tailwindcss @tailwindcss/postcss postcss
    ```
    {{< /tab >}}

    {{< tab label="npm" >}}
    ```bash
    npm install --dev tailwindcss @tailwindcss/postcss postcss
    ```
    {{< /tab >}}

    {{< tab label="yarn" >}}
    ```bash
    yarn add --dev tailwindcss @tailwindcss/postcss postcss
    ```
    {{< /tab >}}

    {{< tab label="pnpm" >}}
    ```bash
    pnpm install --save-dev tailwindcss @tailwindcss/postcss postcss
    ```
    {{< /tab >}}

{{< /tabs >}}

安装完成后，在项目根目录创建postcss.config.mjs文件，并添加以下内容：
```typescript
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};
```
再在项目根目录创建global.css，添加以下内容：
```css
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/preflight.css" layer(base);
@import "tailwindcss/utilities.css";
 
@import "nativewind/theme";
```
### 修改metro.config.js
如果没有metro.config.js文件，请创建一个：
```bash
npx expo customize metro.config.js
```
并添加以下内容：
```typescript
const { getDefaultConfig } = require("expo/metro-config");
const { withNativewind } = require("nativewind/metro");
 
/** @type {import('expo/metro-config').MetroConfig} */
const config = getDefaultConfig(__dirname);
 
module.exports = withNativewind(config);
```
### 引入刚才创建的global.css
- 对于普通RN项目，在App.js中引入global.css
- 对于Expo项目，在app/_layout.tsx中引入global.css
```typescript
// App.js或App.ts或App.jsx或App.tsx
import "./global.css"
export default App() {
  /* Your App */
}
```
### 覆盖lightningcss版本（必须做，否则运行会报错）
官网做法基本正确，但偶有概率报错，所以根据自己项目的react、react-dom、react-native-css版本，添加几项锁定，如下：
{{< tabs >}}

    {{< tab label="npm" >}}

    ```json
    //package.json
    {
      "overrides": {
        "react": "19.1.0",
        "react-dom": "19.1.0",
        "react-native-css": "3.0.1",
        "lightningcss": "1.30.1"
      }
}
    ```
    {{< /tab >}}

    {{< tab label="yarn" >}}
    ```bash
    //package.json
    {
      "resolutions": {
        "react": "19.1.0",
        "react-dom": "19.1.0",
        "react-native-css": "3.0.1",
        "lightningcss": "1.30.1"
      }
}
    ```
    {{< /tab >}}

    {{< tab label="pnpm" >}}
    ```bash
    //package.json
    {
      "pnpm": {
        "overrides": {
          "react": "19.1.0",
          "react-dom": "19.1.0",
          "react-native-css": "3.0.1",
          "lightningcss": "1.30.1"
        }
      }
}
    ```
    {{< /tab >}}

{{< /tabs >}}

### 添加TypeScript支持
项目根目录创建文件nativewind-env.d.ts，添加以下内容：
```typescript
<reference types="react-native-css/types" />
```
### 重新编译启动项目
以上做完后，可能还会有报错，例如：global.css: failed to deserialize; expected an object-like struct named Specifier, found ()
这时候请清理node_modules、pnpm-lock.yaml(或package-lock.json或yarn.lock)，使用你的包管理器重新安装依赖，最好将android文件夹和.expo文件夹也删除，从expo prebuild开始，重新编译启动项目,应该就能解决问题了。