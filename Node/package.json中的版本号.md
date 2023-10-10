#NPM

> https://docs.npmjs.com/cli/v8/configuring-npm/package-json#dependencies

```json
"dependencies": {
    "accepts": "~1.3.7",
    "array-flatten": "1.1.1",
    "body-parser": "^1.19.0",
    "content-disposition": ">0.5.3",
    "content-type": "~1.0.4",
    "cookie": "^0.4.0",
    "cookie-signature": "<1.0.6",
    "debug": ">=2.6.9",
    "depd": "~1.1.2",
    "encodeurl": "<1.0.2"
}
```

其中依赖名前会加上，例如 `~ ^ >= < + *` 这些符号

版本号规则：主版本号.次版本号.修补版本号 major.minor.patch
- major：新的架构调整，不兼容老版本
- minor：新增功能，兼容老版本
- patch：修复bug，兼容老版本


`version`: 必须是`version`版本
`~version`: 更新到minor中最新的版本
`^version`: 更新到major中最新的版本
`latest`: 更新到最新版
`*`: 任意版本
`>version`: 必须大于某个版本
`<version`: 必须小于于某个版本
`1.2.x`: 可以是 1.2.0, 1.2.1, 但是不能是 1.3.0
`user/repo`: github仓库地址
`path/path`: 本地目录路径