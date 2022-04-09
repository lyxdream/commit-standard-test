1. 规范工具

npm install commitizen cz-conventional-changelog -D
```json
 "scripts": {
    "commit": "cz"
  },
  "config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
```
npm install  git-cz --save-dev

新增 changelog.config.js

```json
 "scripts": {
    "commit": "git-cz"
  },
```
2. 校验规则

```
 npm i @commitlint/cli @commitlint/config-conventional -D
```
在项目中新建 commitlint.config.js 文件并设置校验规则：

```
module.exports = {
    // commit lint 校验规则继承
    extends: ['@commitlint/config-conventional'],
    // 自定义校验规则
    rules: {},
}
```
3. 规范校验

```
npm i  husky -D

```

```json
"husky": {
    "hooks": {
        "pre-commit": "npm run lint",
        "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
}

```

4. 生成日志

测试
