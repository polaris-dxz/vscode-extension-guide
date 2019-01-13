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


## VSCode 常用插件

| 名称                                                         | 简述                                               |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag) | 自动闭合HTML标签                                   |
| [Auto Import](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport) | import提示                                         |
| [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag) | 修改HTML标签时，自动修改匹配的标签                 |
| [Babel JavaScript](https://marketplace.visualstudio.com/items?itemName=mgmcdermott.vscode-language-babel) | babel插件，语法高亮                                |
| [Babelrc](https://marketplace.visualstudio.com/items?itemName=waderyan.babelrc) | .babelrc文件高亮提示                               |
| [Beautify css/sass/scss/less](https://marketplace.visualstudio.com/items?itemName=michelemelluso.code-beautifier) | css/sass/less格式化                                |
| [Better Align](https://marketplace.visualstudio.com/items?itemName=wwm.better-align) | 对齐赋值符号和注释                                 |
| [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments) | 编写更加人性化的注释                               |
| [Bookmarks](https://marketplace.visualstudio.com/items?itemName=alefragnani.Bookmarks) | 添加行书签                                         |
| [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) | 用不同颜色高亮显示匹配的括号                       |
| [Can I Use](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-caniuse) | HTML5、CSS3、SVG的浏览器兼容性检查                 |
| ~~Code Outline~~                                             | ~~展示代码结构树~~                                 |
| [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) | 运行选中代码段（支持多数语言）                     |
| [Code Spell checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) | 单词拼写检查                                       |
| [CodeBing](https://marketplace.visualstudio.com/items?itemName=SirTobi.code-bing) | 快速打开Bing并搜索，可配置搜索引擎                 |
| [Color Highlight](https://marketplace.visualstudio.com/items?itemName=naumovs.color-highlight) | 颜色值在代码中高亮显示                             |
| [Color Info](https://marketplace.visualstudio.com/items?itemName=bierner.color-info) | 小窗口显示颜色值，rgb,hsl,cmyk,hex等等             |
| [Color Picker](https://marketplace.visualstudio.com/items?itemName=anseki.vscode-color) | 拾色器                                             |
| [CSS-in-JS](https://marketplace.visualstudio.com/items?itemName=paulmolluzzo.convert-css-in-js) | CSS-in-JS高亮提示和转换                            |
| [Dash](https://marketplace.visualstudio.com/items?itemName=deerawan.vscode-dash) | 集成Dash                                           |
| [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) | 调试Chrome                                         |
| [Document This](https://marketplace.visualstudio.com/items?itemName=joelday.docthis) | 注释文档生成                                       |
| [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv) | .env文件高亮                                       |
| [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) | EditorConfig插件                                   |
| [Emoji](https://marketplace.visualstudio.com/items?itemName=Perkovec.emoji) | 在代码中输入emoji                                  |
| [endy](https://marketplace.visualstudio.com/items?itemName=c75.endy) | 将输入光标跳转到当前行最后面                       |
| [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) | ESLint插件，高亮提示                               |
| [File Peek](https://marketplace.visualstudio.com/items?itemName=abierbaum.vscode-file-peek) | 根据路径字符串，快速定位到文件                     |
| [filesize](https://marketplace.visualstudio.com/items?itemName=mkxml.vscode-filesize) | 状态栏显示当前文件大小                             |
| [Find-Jump](https://marketplace.visualstudio.com/items?itemName=mksafi.find-jump) | 快速跳转到指定单词位置                             |
| [Font-awesome codes for html](https://marketplace.visualstudio.com/items?itemName=medzhidov.font-awesome-codes-html) | FontAwesome提示代码段                              |
| [ftp-sync](https://marketplace.visualstudio.com/items?itemName=lukasz-wronski.ftp-sync) | 同步文件到ftp                                      |
| [Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame) | 在状态栏显示当前行的Git信息                        |
| [Git History(git log)](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory) | 查看git log                                        |
| [gitignore](https://marketplace.visualstudio.com/items?itemName=codezombiech.gitignore) | .gitignore文件语法                                 |
| [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) | 显示文件最近的commit和作者，显示当前行commit信息   |
| [GraphQL for VSCode](https://marketplace.visualstudio.com/items?itemName=kumar-harsh.graphql-for-vscode) | graphql高亮和提示                                  |
| [Guides](https://marketplace.visualstudio.com/items?itemName=spywhere.guides) | 高亮缩进基准线                                     |
| [Gulp Snippets](https://marketplace.visualstudio.com/items?itemName=tanato.vscode-gulp) | Gulp代码段                                         |
| [HTML CSS Class Completion](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) | CSS class提示                                      |
| [HTML CSS Support](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css) | css提示（支持vue）                                 |
| [HTMLHint](https://marketplace.visualstudio.com/items?itemName=mkaufman.HTMLHint) | HTML格式提示                                       |
| [htmltagwrap](https://marketplace.visualstudio.com/items?itemName=bradgashler.htmltagwrap) | 快捷包裹html标签                                   |
| [htmltagwrap](https://marketplace.visualstudio.com/items?itemName=bradgashler.htmltagwrap) | 包裹HTML                                           |
| [Import Beautify](https://marketplace.visualstudio.com/items?itemName=varharrie.import-beautify) | import分组、排序、格式化                           |
| [Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost) | 行内显示导入（import/require）的包的大小           |
| [Indenticator](https://marketplace.visualstudio.com/items?itemName=SirTori.indenticator) | 缩进高亮                                           |
| [IntelliSense for css class names](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) | css class输入提示                                  |
| [JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets) | ES6语法代码段                                      |
| [JavaScript Standard Style](https://marketplace.visualstudio.com/items?itemName=chenxsan.vscode-standardjs) | Standard风格                                       |
| [JS Refactor](https://marketplace.visualstudio.com/items?itemName=cmstead.jsrefactor) | 代码重构工具，提取函数、变量重命名等等             |
| [JSON to TS](https://marketplace.visualstudio.com/items?itemName=MariusAlchimavicius.json-to-ts) | JSON结构转化为typescript的interface                |
| [JSON Tools](https://marketplace.visualstudio.com/items?itemName=eriklynd.json-tools) | 格式化和压缩JSON                                   |
| [jumpy](https://marketplace.visualstudio.com/items?itemName=wmaurer.vscode-jumpy) | 快速跳转到指定单词位置                             |
| [language-stylus](https://marketplace.visualstudio.com/items?itemName=sysoev.language-stylus) | Stylus语法高亮和提示                               |
| [Less IntelliSense](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-less) | less变量与混合提示                                 |
| [Lodash](https://marketplace.visualstudio.com/items?itemName=oysun.Lodash) | Lodash代码段                                       |
| [Log Wrapper](https://marketplace.visualstudio.com/items?itemName=chrisvltn.log-wrapper-for-vscode) | 生产打印选中变量的代码                             |
| [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) | Markdown格式提示                                   |
| [MochaSnippets](https://marketplace.visualstudio.com/items?itemName=Alan.MochaSnippets) | Mocha代码段                                        |
| [Node modules resolve](https://marketplace.visualstudio.com/items?itemName=naumovs.node-modules-resolve) | 快速导航到Node模块                                 |
| [npm](https://marketplace.visualstudio.com/items?itemName=fknop.vscode-npm) | 运行npm命令                                        |
| [npm Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense) | 导入模块时，提示已安装模块名称                     |
| [Output Colorizer](https://marketplace.visualstudio.com/items?itemName=IBM.output-colorizer) | 彩色输出信息                                       |
| [Partial Diff](https://marketplace.visualstudio.com/items?itemName=ryu1kn.partial-diff) | 对比两段代码或文件                                 |
| [Path Autocomplete](https://marketplace.visualstudio.com/items?itemName=ionutvmi.path-autocomplete) | 路径完成提示                                       |
| [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) | 另一个路径完成提示                                 |
| [Polacode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode) | 将代码生成图片                                     |
| [PostCss Sorting](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-postcss-sorting) | css排序                                            |
| [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) | prettier官方插件                                   |
| [Prettify JSON](https://marketplace.visualstudio.com/items?itemName=mohsen1.prettify-json) | 格式化JSON                                         |
| [Project Manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager) | 快速切换项目                                       |
| [Quokka.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode) | 不需要手动运行，行内显示变量结果                   |
| [React Native Storybooks](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-react-native-storybooks) | storybook预览插件，支持react                       |
| [React Playground](https://marketplace.visualstudio.com/items?itemName=wmira.react-playground-vscode) | 为编辑器提供一个react组件运行环境，方便调试        |
| [React Standard Style code snippets](https://marketplace.visualstudio.com/items?itemName=TimonVS.ReactSnippetsStandard) | react standar风格代码块                            |
| [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) | 发送REST风格的HTTP请求                             |
| [Sass](https://marketplace.visualstudio.com/items?itemName=robinbentley.sass-indented) | sass插件                                           |
| [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) | VSCode设置同步到Gist                               |
| [Sort lines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines) | 排序选中行                                         |
| [Sort Typescript Imports](https://marketplace.visualstudio.com/items?itemName=miclo.sort-typescript-imports) | typescript的import排序                             |
| [String Manipulation](https://marketplace.visualstudio.com/items?itemName=marclipovsky.string-manipulation) | 字符串转换处理（驼峰、大写开头、下划线等等）       |
| [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint) | css/sass/less代码风格                              |
| [SVG Viewer](https://marketplace.visualstudio.com/items?itemName=cssho.vscode-svgviewer) | SVG查看器                                          |
| [Syncing](https://marketplace.visualstudio.com/items?itemName=nonoroazoro.syncing) | vscode设置同步到gist                               |
| [Test Spec Generator](https://marketplace.visualstudio.com/items?itemName=rintoj.chai-spec-generator) | 测试用例生成（支持chai、should、jasmine）          |
| [TODO Parser](https://marketplace.visualstudio.com/items?itemName=minhthai.vscode-todo-parser) | Todo管理                                           |
| [TS/JS postfix completion](https://marketplace.visualstudio.com/items?itemName=ipatalas.vscode-postfix-ts) | ts/js后缀提示                                      |
| [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint) | TypeScript语法检查                                 |
| [Types auto installer](https://marketplace.visualstudio.com/items?itemName=jvitor83.types-autoinstaller) | 自动安装[@types](https://github.com/types)声明依赖 |
| [TypeScript Hero](https://marketplace.visualstudio.com/items?itemName=rbbit.typescript-hero) | TypeScript辅助插件，管理import、outline等等        |
| [TypeScript Import](https://marketplace.visualstudio.com/items?itemName=kevinmcgowan.TypeScriptImport) | TS自动import                                       |
| [TypeScript Import Sorter](https://marketplace.visualstudio.com/items?itemName=mike-co.import-sorter) | import整理排序                                     |
| [Typescript React code snippets](https://marketplace.visualstudio.com/items?itemName=infeng.vscode-react-typescript) | React Typescript代码段                             |
| [TypeSearch](https://marketplace.visualstudio.com/items?itemName=lucasschejtman.vscode-typesearch) | TS声明文件搜索                                     |
| [Version Lens](https://marketplace.visualstudio.com/items?itemName=pflannery.vscode-versionlens) | package.json文件显示模块当前版本和最新版本         |
| [vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur) | 目前比较好的Vue语法高亮                            |
| [View Node Package](https://marketplace.visualstudio.com/items?itemName=dkundel.vscode-npm-source) | 快速打开选中模块的主页和代码仓库                   |
| [VS Live Share](https://marketplace.visualstudio.com/items?itemName=ms-vsliveshare.vsliveshare) | 实时多人协助                                       |
| [VSCode Great Icons](https://marketplace.visualstudio.com/items?itemName=emmanuelbeziat.vscode-great-icons) | 文件图标拓展                                       |
| [vscode-database](https://marketplace.visualstudio.com/items?itemName=bajdzis.vscode-database) | 操作数据库，支持mysql和postgres                    |
| [vscode-icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons) | 文件图标，方便定位文件                             |
| [vscode-random](https://marketplace.visualstudio.com/items?itemName=jrebocho.vscode-random) | 随机字符串生成器                                   |
| [vscode-spotify](https://marketplace.visualstudio.com/items?itemName=shyykoserhiy.vscode-spotify) | 集成spotify，播放音乐                              |
| [vscode-styled-components](https://marketplace.visualstudio.com/items?itemName=jpoissonnier.vscode-styled-components) | styled-components高亮支持                          |
| [vscode-styled-jsx](https://marketplace.visualstudio.com/items?itemName=blanu.vscode-styled-jsx) | styled-jsx高亮支持                                 |
| [Vue TypeScript Snippets](https://marketplace.visualstudio.com/items?itemName=ducksoupdev.Vue2) | Vue Typescript代码段                               |
| [VueHelper](https://marketplace.visualstudio.com/items?itemName=oysun.vuehelper) | Vue2代码段（包括Vue2 api、vue-router2、vuex2）     |
| [Wallaby.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.wallaby-vscode) | 实时测试插件                                       |

