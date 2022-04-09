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

