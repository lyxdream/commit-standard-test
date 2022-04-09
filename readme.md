# 
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
npm i lint-staged -D 

```
tip: "husky": "^4.3.0" 高版本的不生效

```json
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
   "lint-staged": {
    "./**/*.{js}": [
      "eslint --fix",
      "git add"
    ]
  },
```

使用高版本的husky

```
npm install husky -D

在控制台输入命令，生成.husky文件夹：
npx husky install


npm i lint-staged -D 
```

- 使用commit-msg钩子规范化提交信息

.husky/commit-msg

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx --no-install commitlint --edit $1
```

- 使用pre-commit检测提交时代码规范

.husky/pre-commit

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npm run eslint
```

```
  "scripts": {
    "eslint": "eslint src",
    "commit": "git-cz"
  },

```

- 使用lint-staged自动修复格式错误

```
npm install lint-staged  -D
```

在package.json中添加配置：

```json
"lint-staged": {
    "./**/*.{js}": [
        "eslint --fix",
        "git add"
    ]
}
```
然后修改 .husky/pre-commit 文件：

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```
这个过程lint-staged做了两个事情：

1)如果符合规则：则会提交成功。
2)如果不符合规则：它会自动执行 eslint --fix 尝试帮你自动修复，如果修复成功则会帮你把修复好的代码提交，如果失败，则会提示你错误，让你修好这个错误之后才能允许你提交代码。

代码被修复了，并将test.js提交到了暂存区。
4. 生成日志

