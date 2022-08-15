安装：

npm i -g typescript

输入tsc出现一大堆东西证明安装成功

| 类型 | 说明 |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |

tsc  xxx.ts -w

tsconfig.json是ts编译器的配置文件，ts编译器可以根据tsconfig的信息对ts代码进行编译

```
//'include'用来指定哪些ts文件需要被编译
"include":['./src/**/*'] //src下的任意目录下的任意文件
//'exclude'用来指定哪些ts文件不需要被编译（排除一些文件），有默认值
"complierOptions": {
//'target'用来指定ts编译为es的版本：
//es3,es5,es6,es2015,es2016,es2017,es2018,es2019,es2020,es2021,esnext
'target':"esnext"//最新版本
//'module' 指定要使用的模块化的规范
//nonhe,commonjs,amd,es6,es2015,es2020,esnext,umd,system
//'lib' 指定要使用的库，有默认值，一般不配置
//'outDir' 用来指定编译后文件所在的目录
'outDir':'./dist
//'outfile' 将代码合并成一个文件，只在module为commonjs和system时可用
//'allowJs' 是否对js文件进行编译，默认为false
//'checkJs' 是否对js代码进行语法检查，默认为false
//'removeComments' 编译后是否保留注释，默认为true
//'noEmit' 不生成编译后的文件，默认为false
//'noEmitOnError' 当有错误时不生成编译后的文件，默认为false

//----------关于语法检查的配置
//'alawysStrict' 编译后的文件是否使用严格模式，默认false
//'noImplicitAny' 不允许隐式any类型，默认false
//'noImplicitThis' 不允许隐式this类型，默认false
//'strictNullChecks' 严格检查null类型，对有可能是null类型的后续操作进行报错
//'strict' 所有严格检查的总开关，是true的话所有严格检查全部打开，false则全部关闭，yi'na
}
```

