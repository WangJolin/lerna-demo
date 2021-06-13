# Lerna Demo

## Lerna 是什么?

-   [Lerna is a tool that optimizes the workflow around managing multi-package repositories with git and npm.](https://lerna.js.org/)
-   **Lerna** 是用来优化使用 git 和 npm 管理的**多包仓库**工作流的一个**工具**。

## 为什么有 Lerna?

> 假如现有一个大型工程项目 P，P 依赖于 npm 包 A、B、C，其中 A 依赖于 B 和 C，C 依赖于 B 和 A。那么就会面临如何管理这些包的问题。解决方式有两种：Multirepo 和 Monorepo。

-   `Multirepo`：**多代码**仓库。按模块分为多个代码库。多个依赖库进行**独立管理**。允许各个模块有自己的一套玩法（依赖管理、单元测试等）。每个库有更新时，需要先发布，然后再去安装使用。显而易见，**依赖关系越复杂项目越难维护**。

-   `Monorepo(monolithic repository)`：**单代码**仓库。强调集中管理。Monorepo 将所有的模块都放在一个仓库中，每个模块单独发布，但使用与仓库一致的版本号。

## Lerna 使用

### 1. 使用

```git
npm install --global lerna // 全局安装 lerna
git init lerna-repo && cd lerna-repo // git init 新建仓库
lerna init // 初始化项目
```

初始化后的项目目录如下：

```
lerna-repo/
  packages/
  package.json
  lerna.json
```

### 2. 管理模式

-   固定模式：`lerna init`。通过`lerna.json`里的版本进行统一的版本管理。这种模式自动将所有 `packages` 包版本捆绑在一起，对任何其中一个或者多个 `packages` 进行重大改动都会导致所有 `packages` 的版本号进行升级。
-   独立模式： `lerna init --independent`。允许使用者对每个 `package` 单独改变版本号。每次执行 `lerna publish` 的时候，针对所有有更新的 `package`，会逐个询问需要升级的版本号，基准版本为它自身的 `package.json` 里面的版本号。这种情况下，`lerna.json` 的版本号不会变化， 默认为 `independent`。

### 3. 常用命令

-   `lerna init`：创建一个新的 lerna 存储库或将现有存储库升级到 Lerna 的当前版本。
-   `lerna bootstrap`：引导当前 Lerna 存储库中的包。安装它们的所有依赖项并链接任何交叉依赖项。
-   `lerna import <pathToRepo>`：将本地路径 \<pathToRepo> 中的包导入到带有提交历史记录的包/\<directory-name> 中。例如：，`lerna import ~/Users/Product --dest=utilities`是将路径为`~/Users/Product`的包导入到名为`utilites`的包中。
-   `lerna add xxx`：添加依赖。参数 `--scope=pkgName`。
    -   在所有 `package` 中安装 `react`： `lerna add react`
    -   仅在 `tools` 中安装 `lodash` `lerna add lodash --scope=app`
    -   将 `ui` 关联到 `app` lerna add ui --scope=app

参考：

-   [官网](https://lerna.js.org/)
-   [lerna 多包管理实践](https://juejin.cn/post/6844904194999058440#heading-0)
-   [lerna 入门](https://juejin.cn/post/6844904116477493256#heading-0)
-   [文档](https://github.com/chinanf-boy/lerna-zh)
