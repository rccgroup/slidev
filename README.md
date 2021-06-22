## 文档
- [Slidev](https://cn.sli.dev/)
- [开始使用 | Slidev](https://cn.sli.dev/guide/#features)

## node 版本
```
Slidev 需要 Node.js 的版本 >=14.0.0

可以使用这个版本：
nvm use v16.2.0
```

## 操作提示
```ruby
npx slidev --help

命令：
  slidev [entry]             Start a local server for Slidev            [默认值]
  slidev build [entry]       Build hostable SPA
  slidev export [entry]      Export slides to PDF
```

注意打包是的一些参数：
```
npx slidev build 'markdowns/learn_ruby.md' --base="/xx-project/learn_ruby" --out='docs/learn_ruby'
```

具体命令行参数，可以查看 slidev 源码的 `packages/slidev/node/cli.ts`

相关已有命令，可以查看 `package.json` :
```
"scripts": {
    "dev": "slidev --open",
    "build": "slidev build",
    "export": "slidev export",
    "png": "slidev export --format png"
}
```

## 例子
比如，现在如果需要新增一个样式文稿，只需要在 `markdowns` 文件新增一个 `markdown` 文件，假如叫做（`some_example.md`） 。

然后就可以启动预览：
- `npx slidev 'markdowns/some_example.md'`
- 或者  `npm run dev 'markdowns/some_example.md'`

## 其他配置
如有需要，可以在 `vite.config.ts` 设置。


## 发布到 github pages
在相关项目 —> setting  —> pages，开启托管，执行对应目录即可。

这样，相关的演示文稿即可在线访问。

## 导出
也可以将样式文稿导出为 pdf / png 等格式。

```
slidev export [entry]
slidev export [entry] --format png
```

> 前提：需要额外装个包。
> npm i -D playwright-chromium
>
> [导出 | Slidev](https://cn.sli.dev/guide/exporting.html)


## 本地启动之后，可以在浏览器进行编辑
- [编辑器整合 | Slidev](https://cn.sli.dev/guide/editors.html)

