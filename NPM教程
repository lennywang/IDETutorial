

## NPM 常用命令

### npm install

**安装包，默认会安装最新的版本**

```
npm install gulp
```

**安装指定版本**

```
npm install gulp@3.9.1
```

**-S, --save 安装包信息将加入到dependencies（生产阶段的依赖）**

```markdown
npm install gulp --save 或 npm install gulp -S
```

package.json 文件的 dependencies 字段：

```json
"dependencies": {
    "gulp": "^3.9.1"
}
```



附：

1、依赖包版本号前面 ~或^

* ~会匹配最近的小版本依赖包，比如~1.2.3会匹配所有1.2.x版本，但是不包括1.3.0


* ^会匹配最新的大版本依赖包，比如^1.2.3会匹配所有1.x.x的包，包括1.3.0，但是不包括2.0.0

2、npm i 与npm install

1. 用npm i安装的模块无法用npm uninstall删除，用npm uninstall i才卸载掉 
2. npm i会帮助检测与当前node版本最匹配的npm包版本号，并匹配出来相互依赖的npm包应该提升的版本号 
3. 部分npm包在当前node版本下无法使用，必须使用建议版本 
4. 安装报错时intall肯定会出现npm-debug.log 文件，npm i不一定




> npm 常用命令详解
>
> 参考网址：https://www.cnblogs.com/PeunZhang/p/5553574.html



###  npm ls 

查看全局安装的模块及依赖 

```
npm ls -g 
```

### npm init

在项目中引导创建一个package.json文件

