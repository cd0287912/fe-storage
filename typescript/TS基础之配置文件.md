### 简介

tsconfig.json 文件是 ts 编译器的配置文件，ts 编译器可以根据它的信息来对代码进行编译

### 常见配置参数

```json
{
  // include 用来表示哪些 ts 文件需要被编译
  // ** 表示任意目录，* 表示任意文件
  "include": ["./src/**/*"],
  // exclude 用来表示哪些 ts 文件不需要被编译
  "exclude": [],
  // extends 表示被定义继承的文件
  "extends": "",
  // files 表示被编译文件的列表，只有需要被编译的文件少时才会用到
  "files": [],
  // 编译配置选项
  "compilerOptions": {
    // 用来指定ts被编译为js的版本
    // 'es3', 'es5', 'es6', 'es2015', 'es2016', 'es2017', 'es2018', 'esnext'
    "target": "es5",

    // 指定使用模块化的规范
    // 'none', 'commonjs', 'amd', 'system', 'umd', 'es6', 'es2015', 'esnext'.
    "module": "commonjs",

    // 指定项目中使用的库
    // 值太多，一般不需要指定
    "lib": ["DOM", "es6"],

    // 指定用来编译后文件所在的目录
    "outDir": "./src/dist",

    // 将代码合并为一个文件
    // 设置后，将所有的作用域中的代码合并到同一个文件中
    // 一般不设置
    "outFile": "",

    // 指定是否对js的编译，默认为false
    "allowJs": false,

    // 指定是否检查js语法是否规范，默认为false
    "checkJs": false,

    // 指定是否移除注释
    "removeComments": false,

    // 指定不生成编译后的文件
    "noEmit": false,

    // 指定有错误时不生成编译后的文件
    "noEmitOnError": false,

    // ==========语法相关==============

    // 指定编译后的文件是否启动严格模式
    "alwaysStrict": false,

    // 指定是否开启隐式any类型
    "noImplicitAny": true,

    // 指定不允许不明确的this
    "noImplicitThis": false,

    // 指定是否严格的空值检查
    "strictNullChecks": true,

    // 严格检查的总开关
    "strict": true
  }
}
```
