## gulp简单介绍 —— 庞伟湛PAM ##

#### *目录*
1. gulp简介
1. nodejs和npm
1. 创建一个npm项目 —— npm init .
1. 为我的项目安装npm插件 —— npm install ***
1. gulp编写简述 —— gulp.***
1. 在我的项目中使用gulp —— (ejs + sass)
1. 我认为的文件目录结构 —— app, build*
1. 我爱用的gulp插件
1. 寻找好用的gulp插件 —— cnpmjs.org

<hr>

### 1. gulp简介 ###
引入百度链接
gulp是一块自动化构建工具。

<hr>

### 2. nodejs和npm ###
引入nodejs下载地址，介绍win7下的安装方法，如何设置环境变量。同时介绍npm，node package manager。</br>

同时，您需要一个**命令行环境**来执行nodejs的命令。</br>
	- 在windows下，我推荐使用PowerCmd来进行window的原生命令行环境，它可以在一个窗口内同时启动多个cmd进程。</br>
	- 同时推荐安装git bash来进行类linux的命令环境，我们也可以通过git bash来进行git的命令行操作。</br>

<hr>

### 3. 创建一个npm项目 —— npm init . ###
我们可以通过在命令行中输入：`node init yourDir`来实现一个基本项目的创建。</br>

下面我将演示如何创建一个npm管理项目。</br>

	// 假设我正处于F盘，并使用git bash命令行环境
1. `mkdir test` *//创建文件夹test*
1. `cd test`	*//进入到test文件夹中*
1. `npm init .` *//创建npm管理项目*
1. 根据提示输入信息(包括name, version, description等)，直接按**回车**可以选择默认输入。
1. 信息录入完整后，会出现整个package.json的内容，确认无误后，输入**yes**完成项目创建。
1. 这时候我们会发现test目录下多了package.json文件。
	1. "devDependencies"与"dependencies"。
	2. 在package.json中，"devDependencies"这一项意味着所安装的插件是开发所依赖的插件，在正式上线时不会用上。
	2. 而"dependencies"这一项意味着所安装的插件是生产所依赖的插件，是使用于生产环境中的。

<hr>

### 4. 为我的项目安装npm插件 —— npm install *** ###
通过在命令行中输入  `npm install plugIn__name`  来进行nodeJS插件的安装，例如gulp插件：`npm install gulp --save-dev`。

其中我们可以在命令的后面加上各种参数，来实现我们想要的效果。例如：

	// 以下均以安装gulp插件为例
1. `npm install` 可以缩写为`npm i`。
1. `npm i gulp -g`
	- `-g`意味着在全局范围内安装gulp插件。
	- gulp插件会被安装在c盘下的global_modules中。
	- 安装完成后，在电脑的任意npm项目中，我们都可以使用到所安装的gulp插件，意味着，gulp插件已经**全局化**了。
1. `npm i gulp --save-dev`。 
	- 命令执行完后，打开package.json，发现`"devDependencies"`下多了`"gulp": "^3.9.0"`这一项。
	- `--save-dev`意味着我们会将gulp插件安装在开发依赖下，也就是"devDependencies"中了。
1. `npm i gulp --save`。
	- 本命令`--save`与`--save-dev`属于同类型命令，都会改写package.json的中的依赖列表。
	- 命令执行完后，打开package.json，发现`"devDependencies"`下多了`"gulp": "^3.9.0"`这一项。
	- `--save-dev`意味着我们会将gulp插件安装在生产依赖下，也就是"dependencies"中。

待补充待补充待补充待补充待补充待补充待补充待补充待补充

<hr> 

### 5. gulp编写简述 —— gulp.*** ###

gulp的方法非常简单，只有5中，分别是：

gulp.src
gulp.dest
1. gulp.task:
1. gulp.watch:
1. gulp.

<hr>

### 6. 在我的项目中使用gulp —— (ejs + sass) ###

html
---
在开发“后台语音在线系统”时，我深深的感到了html模板化的重要性。结合之前自己的一些个人心得，我在进行“奇迹战神”的移动端官网时，做了大胆的尝试，将传统的*.html使用模板工具代替。

使用另类模板取替传统的*.html有如下好处：
> 1、实现html组件化。我们可以将一个html页面拆分成很多的模板，通过导入实现引用。</br>
> 2、实现内容变量化。例如每一个页面的title等。</br>
> 3、实现html中嵌入程序性语言，例如if语句，for语句等。

#### jade ####
一开始所使用的，是**jade模板**。jade是一款非常简洁的模板化工具，能让我们远离标签化的html书写格式。但在本人使用下来，由于：
> 1、全新的书写习惯，学习成本高，团队迁移难度更大；</br>
> 2、jade编译后的文档，展开之后，并不能如我所愿的将所有元素都按照想要的形式美化，而是“内联元素会跟随在块级元素内”。强迫症的我找了很多Html美化的插件，均无法解决此问题。

因此，**放弃使用jade**。


#### ejs ####
接着尝试着使用了**ejs模板**。ejs较之html相比，在格式和内容上并没有太多的差别，感觉更像是在html的基础之上进行的功能性优化，其中包括：
> 1、html模板化，例如header和footer这类通用性的组件，我们从此可以直接导入即可，非常方便。同时，我们也可以实现**组件化开发**。</br>
> 2、通过ejs生成出来的文件，可以保持原有的编辑格式，通过拼凑的形式实现html的生成。强迫症的我从此不用再让妈妈担心啦~ </br>

但是ejs也是有其缺点的，主要体现在其繁琐的变量书写格式上。`<% ... %>`尖括号与百分号结合的变量格式让我吐槽不已，比起`{{ ... }}`的双大括号格式，复杂了很多。

#### art template ####
art template原先我是并不清楚的，经过勇哥介绍之后，我才恍如隔世的回去开始深入理解这一个html模板。研究结果如下：
> 1、art template是由腾讯上海研究中心(没有猜错，即张鑫旭所在地)所创作的。</br>
> 2、本模板是通过js的方式进行编译，具有高性能、简洁易用的优点。(这是官方介绍，实际我并没有深入理解，如有偏颇，请不要打我。) </br>
> 3、art template结合了ejs和jade的优点，在html标记化格式的基础之上，同时兼容`<% ... %>`和`{{ ... }}`的变量写法，我认为非常的方便。
> 4、关于art template这一块，在gulp上并没有很好的构建插件，只有一个没有介绍的gulp-arttemplate插件。由于没有介绍，无法知晓该插件的使用方法，因此作废。

综上，最终选定使用ejs作为html模板，但是art template潜力巨大。

CSS
---
关于css上，因为团队一直在使用sass + compass，所以选定sass + compass来作为css模板，所使用的gulp插件为： **gulp-ruby-sass**。

js
---
由于并没有接触到太深的js编写，因此没有选定js的编写格式。还请各位指点一下，让我更好的选定js的模板。

目前gulp可以通过插件，实现js的压缩/丑化，语法检查，合并，打包等功能，还有更多上面没有讲到，但是需要的，也请跟我说说哦，我回去查查看有没有相应的插件可供使用。

<hr>

### 7. 我认为的文件目录结构 —— app, build* ###

在“奇迹战神”官网中，我尝试着探索了许多的文档目录结构。

由于gulp是一个自动化构建工具，它会把我们写好的开发文件逐一经过指定任务进行处理，形如 *.ejs 最终被输出成 *.html， *.scss 最终被输出成 *.css。

结合需求与gulp的特性，并多番思考，我认为对于我们的项目而言，以下目录结构是最为合适的。

在主目录下，目录结构如下：

	- /app			//存放构建前的文件。这是我们手写代码主要存放的位置
		- *.ejs
		- ejsData.json
		- /style
			- *.css
		- /images
			- *.{ png, jpg, ... }
	- /build			//存放构建后的文件
		- *.html			//ejs构建后生成的html文件
		- /css			
			- *.css			// /style目录中的*.scss文件构建后存放与此
		- /js
			- *.js			//尚未实现构建，所有的js文件直接编辑并存放于此。
		- /images
			- *.{ png, jpg, ... }	//存放经过imagemin压缩后的图片
	- /node_modules		//nodeJS的插件存放位置
	- gulpfile.js		//gulp的配置文件
	- package.json		//nodeJs的配置文件
	- congif.rb			//compass的配置文件

