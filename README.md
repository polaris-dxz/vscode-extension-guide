# vscode-extension-guide
## 项目启动

1. 首先安装 yeoman 和 vscode generator脚手架（该项目是基于nodejs的，这里假设你已经装好node环境了）

	```shell
	# 安装 yeoman 和 generator-code 脚手架
	npm install -g yo generator-code
	```

2. 用脚手架快速生成项目文件，按照提示正常填就可以了，这里我选择的是开发插件，语言我选择的是JavaScript

	```shell
	# 利用脚手架快速生成项目
	yo code
	#? What type of extension do you want to create? New Extension (JavaScript)
	#? What's the name of your extension? vscode-hello-world-demo
	#? What's the identifier of your extension? vscode-hello-world-demo
	#? What's the description of your extension? hello world demo
	#? Enable JavaScript type checking in 'jsconfig.json'? No
	#? Initialize a git repository? No
	#? Which package manager to use? npm
	```
![yo code 脚手架](https://github.com/Yggdrasill-7C9/vscode-extension-guide/blob/master/screenshot/yo-code.png)

3. 安装项目所需要的依赖

	```shell
	npm install
	```
	
4. 项目结构如下：

	```php
	.
	├── CHANGELOG.md ## 修改记录
	├── README.md ## 插件说明 README
	├── extension.js ## 入口文件
	├── jsconfig.json ## JavaScript 配置
	├── node_modules ## 依赖
	├── package-lock.json
	├── package.json 
	├── test # 测试环境
	└── vsc-extension-quickstart.md ## 快速启动说明文档
	```

5. 配置文件 package.json

	具体详细说明请看[官方文档](https://code.visualstudio.com/api/references/extension-manifest)


	```json
	
	{   

		"name": "helloworld",// 项目名称
		"displayName": "helloworld", //插件名称
		"description": "",// 项目描述
		"version": "0.0.1",//版本信息
		"engines": {// 启动引擎
			"vscode": "^1.30.0"
		},
		"categories": [
			"Other"
		],
	   // 激活事件列表，列举活跃的命令
		"activationEvents": [
			"onCommand:extension.helloWorld",
			"onCommand:extension.niubi"
		],
	    // 插件入口文件   
		"main": "./extension.js",
		"contributes": {
		// 注册指令信息
			"commands": [
				{
					"command": "extension.helloWorld",
					"title": "Hello World" // 指令名 
				},
				{
					"command": "extension.niubi",
					"title": "niubi"
				}
			]
		},
		"scripts": {
			"postinstall": "node ./node_modules/vscode/bin/install",
			"test": "node ./node_modules/vscode/bin/test"
		},
	    // 开发依赖
		"devDependencies": {
			"typescript": "^3.1.4",
			"vscode": "^1.1.25",
			"eslint": "^4.11.0",
			"@types/node": "^8.10.25",
			"@types/mocha": "^2.2.42"
		}
	}
	
	```

extension.js


	```javascript
	
	/**
	* @param {vscode.ExtensionContext} context
	 */
	function activate(context) {

	    // 使用控制台输出诊断信息
		// 这里的代码只会在插件激活的时候执行一次
		console.log('Congratulations, your extension "helloworld" is now active!');

		// 这个命令在 package.json 中的命令在这里定义
		// 使用 registerCommand 方法来注册实现代码
		// commandId 参数必须与 package.json 匹配

	    // 注册一个命令，命令名为 Hello World (与package.json 中对应)
		let helloworld = vscode.commands.registerCommand('extension.helloWorld', function () {
			// 每次执行命令的时候，都会执行这里的代码

			// 显示信息
			vscode.window.showInformationMessage('Hello World');
		});

	    // 注册一个命令，命令名为 niubi (与package.json 中对应)
		let niubi = vscode.commands.registerCommand('extension.niubi', function () {

			// 显示信息
			vscode.window.showInformationMessage('niubi');
		});

	    // 将刚刚注册的命令 push 到 上下文中
		context.subscriptions.push(helloworld);
		context.subscriptions.push(niubi);
	}
	
	```

## 调试项目

用vscode 打开项目的根目录，按下键盘`F5` 启动调试，这是 vscode 会帮我们开启一个新窗口。

输入`ctrl + shift + p` （mac系统是`cmd + shift + p`） 打开命令面板，

输入 `Hello Wordl` 即可测试我们刚刚编写的指令。



## 打包

打包插件的话需要安装vsce。


	```shell
	
	npm i -g vsce
	
	```

重新编写你插件的README文档，然后在根目录打包后缀为`vsix` 的 vscode 插件。


	```shell
	
	vsve package
	# 如果不修改你插件的readme文档的话会报下面的错误
	# Error: Make sure to edit the README.md file before you publish your extension.
	
	```

## 发布

如果检查你的插件没什么问题了，并且 README 文档和 CHANGELOG 文档已经写的很完善了，

就可以发布到  [ Extension Marketplace ](https://marketplace.visualstudio.com/VSCode) 了。

首先你要注册一个账号，并且获取一个token，然后在命令行输入以下命令就可以了，跟发布 npm 包基本是一样的，这里就不[多做介绍](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)了。 


```shell
vsce create-publisher xxxx
vsce publish
```

## Enjoy It

编写一个vscode 插件的流程大概就是这样，以后遇到坑的话慢慢在[这里](https://github.com/Yggdrasill-7C9/vscode-extension-guide/issues)记录下吧。

祝大家玩得开心！！

