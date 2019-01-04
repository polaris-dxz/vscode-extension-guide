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
![yo code 脚手架](https://github.com/Yggdrasill-7C9/vscode-extension-guide/raw/master/screenshot/yo-code.png)

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
	
		"name": "helloworld",
		"displayName": "helloworld", 
		"description": "",
		"version": "0.0.1",
		"publisher": "ms-vscode",
		"author": {
			"name": "yggdrasill-7c9"
		},
		"engines": {
			"vscode": "^1.30.0"
		},
		"categories": [
			"Other"
		],
		"icon": "images/icon.png",
		"galleryBanner": {
			"color": "#C80000",
			"theme": "dark"
		},
		"activationEvents": [
			"onCommand:extension.helloWorld",
			"onCommand:extension.niubi"
		],
		"main": "./extension.js",
		"contributes": {
			"commands": [
				{
					"command": "extension.helloWorld",
					"title": "Hello World" 
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
		"devDependencies": {
			"typescript": "^3.1.4",
			"vscode": "^1.1.25",
			"eslint": "^4.11.0",
			"@types/node": "^8.10.25",
			"@types/mocha": "^2.2.42"
		},
		"license": "SEE LICENSE IN LICENSE.txt",
		"bugs": {
			"url": "https://github.com/Yggdrasill-7C9/vscode-extension-guide/issues",
			"email": "yggdrasill-7c9@github.com"
		},
		"repository": {
			"type": "git",
			"url": "https://github.com/Yggdrasill-7C9/vscode-extension-guide.git"
		},
		"homepage": "https://github.com/Yggdrasill-7C9/vscode-extension-guide/blob/master/README.md"
	}
	
	```

| 名称                                                         | 是否必须 | 类型                                    | 说明                                                         |
| ------------------------------------------------------------ | -------- | --------------------------------------- | ------------------------------------------------------------ |
| `name`                                                       | 是       | `string`                                | 扩展名 - 应全部小写，不能有空格。                            |
| `version`                                                    | 是       | `string`                                | 版本信息                                                     |
| `publisher`                                                  | 是       | `string`                                | 发布者名字                                                   |
| `engines`                                                    | 是       | `object`                                | 例如：`^0.10.5`表示与最小VS Code版本的兼容性`0.10.5`。       |
| `license`                                                    |          | `string`                                | 请参阅[npm的文档](https://docs.npmjs.com/files/package.json#license)。如果您`LICENSE`的扩展名根目录中有文件，则值`license`应为`"SEE LICENSE IN <filename>"`。 |
| `displayName`                                                |          | `string`                                | 市场中使用的扩展程序的显示名称。                             |
| `description`                                                |          | `string`                                | 您的扩展程序的简要说明。                                     |
| `categories`                                                 |          | `string[]`                              | 要用于扩展的类别允许值： `[Programming Languages, Snippets, Linters, Themes, Debuggers, Formatters, Keymaps, SCM Providers, Other, Extension Packs, Language Packs]` |
| `keywords`                                                   |          | `array`                                 | 一系列**关键字**，以便于查找扩展名。这些包含在Marketplace上的其他扩展**标记中**。此列表目前仅限于5个关键字。 |
| `galleryBanner`                                              |          | `object`                                | 帮助格式化Marketplace标头以匹配您的图标。详情见下文。        |
| `preview`                                                    |          | `boolean`                               | 将扩展名设置为在市场中标记为预览。                           |
| `main`                                                       |          | `string`                                | 您的扩展程序的入口点。                                       |
| [`contributes`](https://code.visualstudio.com/api/references/contribution-points) |          | `object`                                | 描述扩展名[贡献](https://code.visualstudio.com/api/references/contribution-points)的对象。 |
| [`activationEvents`](https://code.visualstudio.com/api/references/activation-events) |          | `array`                                 | 此扩展的[激活事件](https://code.visualstudio.com/api/references/activation-events)数组。 |
| `badges`                                                     |          | `array`                                 | 一系列[已批准的](https://code.visualstudio.com/api/references/extension-manifest#approved-badges)徽章，显示在Marketplace的扩展页面的侧边栏中。每个徽章都是一个包含3个属性的对象：`url`对于徽章的图片网址，`href`用户点击徽章时会关注的链接和`description`。 |
| `markdown`                                                   |          | `string`                                | 控制市场中使用的Markdown渲染引擎。无论是`github`（默认）或`standard`。 |
| `qna`                                                        |          | `marketplace`（默认）`string`,,,`false` | 控制市场中的**问答**链接。设置为`marketplace`启用默认的Marketplace Q＆A网站。设置为字符串以提供自定义问答网站的URL。设置为`false`完全禁用Q＆A。 |
| `dependencies`                                               |          | `object`                                | 您的扩展需要的任何运行时Node.js依赖项。与[npm`dependencies`](https://docs.npmjs.com/files/package.json#dependencies)完全相同。 |
| `devDependencies`                                            |          | `object`                                | 您的扩展需要的任何开发Node.js依赖项。与[npm`devDependencies`](https://docs.npmjs.com/files/package.json#devdependencies)完全相同。 |
| `extensionPack`                                              |          | `array`                                 | 带有此扩展名捆绑的扩展ID的数组。安装主扩展时将安装这些其他扩展。扩展的ID始终是`${publisher}.${name}`。例如：`vscode.csharp`。 |
| `extensionDependencies`                                      |          | `array`                                 | 具有此扩展所依赖的扩展ID的数组。安装主扩展时将安装这些其他扩展。扩展的ID始终是`${publisher}.${name}`。例如：`vscode.csharp`。 |
| `scripts`                                                    |          | `object`                                | 与[npm`scripts`](https://docs.npmjs.com/misc/scripts)完全相同，但具有额外的VS Code特定字段，例如[vscode：](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prepublish-step)[prepublish](https://code.visualstudio.com/api/references/extension-manifest#extension-uninstall-hook)或[vscode：uninstall](https://code.visualstudio.com/api/references/extension-manifest#extension-uninstall-hook)。 |
| `icon`                                                       |          | `string`                                | 图标的路径至少为128x128像素（Retina屏幕为256x256）。         |


​	
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

