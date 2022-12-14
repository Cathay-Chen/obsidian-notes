#git

## 好的 Commit Message 

- 可以使自己或者其他开发人员能够**清晰地知道每个 commit 的变更内容**，方便快速浏览变更历史，比如可以直接略过文档类型或者格式化类型的代码变更。
- 可以基于这些 Commit Message **进行过滤查找**，比如只查找某个版本新增的功能：`git log --oneline --grep "^feat|^fix|^perf"`。
- 可以基于规范化的 Commit Message **生成 Change Log**。
- 可以依据某些类型的 Commit Message **触发构建或者发布流程**，比如当 type 类型为 feat、fix 时我们才触发 CI 流程。
- **确定语义化版本的版本号。** 比如 fix 类型可以映射为 PATCH 版本，feat 类型可以映射为 MINOR 版本。带有 BREAKING CHANGE 的 commit，可以映射为 MAJOR 版本。在这门课里，我就是通过这种方式来自动生成版本号。

##  Angular 规范

Angular 规范其实是一种语义化的提交规范（Semantic Commit Messages），所谓语义化的提交规范包含以下内容：

- Commit Message 是语义化的：Commit Message 都会被归为一个有意义的类型，用来说明本次 commit 的类型。
- Commit Message 是规范化的：Commit Message 遵循预先定义好的规范，比如 Commit Message 格式固定、都属于某个类型，这些规范不仅可被开发者识别也可以被工具识别。

那我们该**怎么写出符合 Angular 规范的 Commit Message 呢**？

在 Angular 规范中，Commit Message 包含三个部分，分别是 Header、Body 和 Footer，格式如下：

```
<type>[optional scope]: <description>
// 空行
[optional body]
// 空行
[optional footer(s)]
```

