# [npm常规命令行集合](https://www.cnblogs.com/cn-andy/p/7091643.html)

最近在摸索vue-cli脚手架的安装，中间用到了一些node的npm命令行，进行了一些整理，并且这个会一直搜集整理更新！

1，常规文件操作命令

cd..          返回当前文件的上一级（向上走）

cd sell        打开"sell"文件夹（向下走）

dir           打开当前文件夹下面的所有文件

F：          直接进入F盘

2，安装文件的命令

npm install <name>             后面接文件名，安装nodejs的依赖包

（可以通过在后面加版本号的方式安装指定版本，如npm install express@3.0.6）

npm install <name>  -g           后面的-g表示将包安装到全局环境中

（直接通过require()的方式是没有办法调用全局安装的包的，全局的安装是供命令行使用的。）

npm install <name> -g --save      后面的--save表示安装的同时，将信息写入package.json中

（项目路径中如果有package.json文件时，直接使用npm install方法就可以根据dependencies配置安装所有的依赖包这样代码提交到github时，就不用提交node_modules这个文件夹了）

npm init                       会引导你创建一个package.json文件，包括名称、版本、作者这些信息等

npm update <name>              更新

npm uninstall <name> --save       删除（删除单个依赖）

**如何删除node_moudle文件夹**

第一步：npm install rimraf -g    

第二步：rimraf node_moudle

**其他一些命令**

npm config set registry https://registry.npm.taobao.org
npm install -g cnpm --registry=https://registry.npm.taobao.org

node -v  验证 node 安装
npm -v  检查 npm 版本
npm install electron-prebuilt --save -dev  安装 electron



# 解决VSCODE"因为在此系统上禁止运行脚本"报错

解决方法：

```
1. 以管理员身份运行vscode;



2. 执行：get-ExecutionPolicy，显示Restricted，表示状态是禁止的;



3. 执行：set-ExecutionPolicy RemoteSigned;



4. 这时再执行get-ExecutionPolicy，就显示RemoteSigned;
```

