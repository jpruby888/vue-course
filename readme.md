# git [git简介 – 李立超 | lilichao.com](https://www.lilichao.com/index.php/2022/11/21/git简介/)

git 菜鸟杀手，

项目的开发是一个不断迭代的过程，开发过程中程序员需要不断的对代码进行编写和更正。这就带来很多的问题。首先，开发中代码会存在多个版本，我们如何将代码在多个版本间进行切换？第二，代码上线后，如何在不影响现行开发工作的情况下对代码进行维护？第三，开发时某段代码被多人修改时，如何处理代码的冲突问题？除此之外，还有存储效率、远程仓库等问题。

git是一个免费开源的版本控制系统，它被设计用来快速高效地管理项目开发的源码。通过git可以跟踪代码的状态，也可以在修改代码后对代码状态进行存储，还可以在需要时将已经修改过的代码恢复到之前存储的状态。更强大的是使用git管理代码时，可以创建代码分支（branch），代码分支相当于一段独立的代码记录，我们可以在分支上对代码进行任意的修改，而这个修改只会影响当前分支，不会对其他分支产生影响。同时，可以对分支进行合并，合并后一个分支的修改便可在另一分支上生效。总之，git是当今最优秀的版本控制工具！

常用命令

```bash
 git commit -a -m '修改三个文件' (修改的文件一次提交，不会提交未跟踪的文件)
 git status
 git log
 git add .
 git commit -m 'message you want to remark'
 git init （初始化仓库）
 git restore * （或者 filename） //从已修改到 未修改状态 重置作用
 git rm <filename> //删除文件
 git rm <filename> -f 强制删除
 git restore --staged <filename> //从暂存状态取消
 git mv from to                 //文件重命名
 // 在自己的分支写代码，没问题就和合并主分支
 git branch # 查看当前分支
git branch <branch name> # 创建新的分支
git branch -d <branch name> # 删除分支
git switch <branch name> # 切换分支
git switch -c <branch name> # 创建并切换分支
git merge <branch name> # 和并分支
```

通过merge合并分时，提交记录就会全部显示，项目比较复杂开发比较波折时反复创建分支反复合并分支，这时候就需要基变。

大部分情况下合并和变基可以呼唤的如果已经提交到远程仓库尽量不要使用变基

```bash
git rebase master #变基到master
```

添加远程仓库名字

github

```bash
git remote add origin https://github.com/jpruby888/git-demo.git
git branch -M main
git push -u origin main
```

gitee

```bash
git remote add gitee https://gitee.com/jpruby/git-demo.git
git push -u gitee "main"
```



## 安装

git的安装十分简单，无脑下一步即可！

下载地址：

win：[32位](https://github.com/git-for-windows/git/releases/download/v2.38.1.windows.1/Git-2.38.1-32-bit.exe) [64位](https://github.com/git-for-windows/git/releases/download/v2.38.1.windows.1/Git-2.38.1-64-bit.exe)

打开命令行，输入`git -v`，能看到正常输出即表示安装成功。

## 配置

查看当前用户用户名和邮箱查看

```bash
git config --global --list 
```

使用git前，我们需要配置一下两个属性name和email，这两个信息会用来在存储代码时记录用户的身份。可以直接在命令行中通过指令来设置：



```bash
git config --global user.name "xxx"
```



```bash
git config --global user.email "xxx"
```

初始化项目：

默认情况下，磁盘中的文件并不由git管理，我们必须要对代码目录进行初始化，初始化后git才能正常的管理文件。进入目录后，直接在目录中执行`git init`即可完成项目的初始化，初始化后目录中会多出一个.git目录，这个目录用来存储代码的版本信息，有了.git就意味着项目现在已经开始被.git管理了，不希望项目被git管理时，只需删除项目中的.git即可。

## 文件状态

git中的文件有两种状态：未跟踪和已跟踪。未跟踪指文件没有被git所管理，已跟踪指文件已被git管理。已跟踪的文件又有三种状态：未修改、修改和暂存。

暂存，表示文件修改已经保存，但是尚未提交到git仓库。

未修改，表示磁盘中的文件和git仓库中文件相同，没有修改。

已修改，表示磁盘中文件已被修改，和git仓库中文件不同。

可以通过`git status`来查看文件的状态

## 基本操作

### 未跟踪 —> 暂存（已跟踪）

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/11/20221121160355310.png)

注：如果你输入git命令后看见了上文的黄色文字，可以执行如下命令来消除：



```bash
git config --global core.fsmonitor true
```

目前目录中存在一个文本文件1.txt，该文件刚刚添加进目录，所以现在文件处于未跟踪（untracked）的状态。如果希望文件交由git管理，需要使用`git add <file>`命令来将文件修改为已跟踪状态：



```bash
git add .\1.txt
```

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/11/20221121161142393.png)

add命令是一个多功能的命令，如果对没有未跟踪的文件调用它会将其设置为已跟踪，并将其转换为暂存状态。如果对已跟踪的文件调用，它就仅仅会将文件设置为暂存状态。

### 暂存 —> 未修改

使用`git commit -m "信息"`，来将暂存的文件提交到git仓库，此时所以暂存文件都变成了未修改的状态。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/11/20221121163807563.png)

使用编辑器对修改状态的文件进行修改，即可使其变为已修改的状态。

### 已修改 —> 暂存

同样调用`add`指令，将已修改文件变为暂存状态。

说的直白些git就是一个存储文件（代码）的仓库，它不仅仅存储了代码，还存储了我们对代码进行的所有的操作。所有的数据在git中会被存储到一个树形结构中。像我们前边的例子中，我们一共commit了三次（初始化一次、修改index.html一次、添加.gitignore一次），我们数据的存储大概是这样一个结构。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182325983.png)commit了三次

每一次的存储就是树上的一个节点，a1表示第一次存储，a2表示第二次存储，a3表示第三次存储，每次存储都会又一个id以便我们可以快速定位，像我们之前通过git log查看时那一长串的字符就是节点的id。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182332778.png)黄色的内容是节点的id

git中存在一个指针被称为HEAD，HEAD表示当前所在的节点。你可以这么理解，树形结构中的一个一个节点就相当于玩单机游戏时存储的一个一个进度，HEAD指向的是当前进度，HEAD指向哪个节点，项目就会变成哪个节点的状态。比如我们在a3时存储了.gitignore，如果我们将HEAD移动到a2节点，由于a2节点时还没有创建文件，所以你会发现项目中的.gitignore会消失不见。（git log中的某个记录后边会跟着一个HEAD，HEAD的位置就表示当前所在的位置）

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182339645.png)HEAD表示当前所在的位置

如何移动HEAD的位置呢？很简单使用`git checkout`命令，checkout的使用方式有很多，比如可以直接在checkout后边跟着节点的id，即可直接将HEAD移动到指定的节点。当然id不需要写完整，只需要写个4-5位即可。如果我们想切换到a2节点，通过log查看可以得知a2节点的id为11210385…。可以通过执行命令`git checkout 1121`切换到a2节点。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182347387.png)切换节点

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182354806.png)此时HEAD移动到了a2节点

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182401651.png)HEAD移动到a2节点，.gitignore消失

通过这种方式可以切换到项目的不同状态，就像单机游戏中的加载进度一样，如此一来我们就可以将代码方便快捷的恢复到不同的状态。

上面说过，git中文件的结构就像是一棵大树，每一次我们对文件的操作就会在树上添加一个节点。默认情况下这棵文件树只有一个主干，这个主干我们称之为master，也就是git中的主分支。当我们checkout 分支名时，会自动回到当前分支的最新节点。所以如果使用`git checkout master`就可以回到主分支的最新节点。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182407845.png)回到主分支

使用`git status`可以查看当前所在的分支。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182414299.png)on branch master表示我们正处在主分支上

也可以通过`git log`来查看。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182420431.png)(HEAD -> master) 表示HEAD的位置，同时表明现在正位于主分支

## 场景一 创建分支

回到虚拟场景中，现在假设我的网站已经编写完毕，正常上线。现在我想在原来网站的基础上开发一些新的功能，但是有不想影响原来的代码，要怎么做？这里我们可以直接创建一个新的分支，所有新的功能都在新分支上进行，好处就是主干于分支是相互独立的，对分支的修改不会影响到主干的内容。

创建新分支：

```
git branch 分支名
```

使用git branch new_site 创建一个新的分支，然后调用`git checkout new_site`切换到新的分支上。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182429194.png)创建并切换到新的分支上

如此一来，我们所有的修改都是在新的分支上进行，不会影响到主分支master上的内容，接下来创建一个新的about.html并提交到新分支上。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182438601.png)对分支进行修改不会影响主分支

此时new_site分支上添加了about.html，在master分支上并没有添加，换句话说new_site分支比master要更快一步，项目在git仓库中发生了分叉，又之前的一个主分支分为了两个分支。如果你愿意可以通过checkout在两个分支间进行切换，直接使用`git checkout 分支名`即可。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182446488.png)使用checkout在不同的分支间进行切换

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182454302.png)现在项目存在两个分支

## 场景二 合并分支

好了现在新版本的网站开发完毕，现在我需要将新添加的内容合并到master（主分支）中，由于项目本身结构简单所以合并起来也是非常容易。首先需要先使用checkou切换回主分支。然后调用`git merge 分支名`来将其合并到主分支中。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182502863.png)将new_site合并到主分支中

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182518901.png)master（主分支）和new_site合并到了一起

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182525162.png)结构示意

合并后new_site分支已经没有存在的意义，可以使用`git branch -d 分支名`将其删除。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182532798.png)删除new_site分支

## 场景三 更加复杂的情况

上边的场景是合并分支最简单的场景，两个分支中的文件没有任何的冲突（没有同时修改同一个文件），现在我们看一种相对复杂一些的情况。

现在我们通过`git checkout -b 分支名`创建一个新分支，该指令用户创建并切换到一个新的分支，相当于branch+checkout。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182610346.png)创建并切换到test分支

然后在test分支中对index.html进行修改并提交。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182621260.png)在test分支中对index.html进行修改

然后切换回master分支，同样对index.html进行修改并提交。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182628961.png)在master中对index.html进行修改并提交

现在我们在两个分支中，都对index.html进行了修改，由此情况变得稍微复杂一些，存储结构大致如下：

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182635827.png)两个分支都对同一个文件进行修改并提交

虽然情况变得复杂，但是步骤还是大体类似，先切换到master分支，然后调用merge进行合并。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182648479.png)合并时出现问题

合并时提示错误，CONFLICT (content): Merge conflict in index.html，conflict表示冲突，git尝试合并文件时发现冲突（因为两个分支都对该文件进行了修改）。首先git回尝试自动合并。Automatic merge failed; fix conflicts and then commit the result.表示自动合并失败，git无法处理这个问题，我们需要手动处理，此时打开发生冲突的文件index.html，会出现如下内容：

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182657483.png)发生冲突后文件内容被修改

在`<<<<<<< HEAD`和`>>>>>>>>test`中间的内容就表示发生冲突的内容，====上边的是当前分支中的代码，====后边的是被合并分支的代码，这是这段内容的冲突导致git不知道如何处理，这里我们需要手动解决冲突，根据不同需要处理方式也不同，而我期望保留两次的修改所以我直接将冲突的标识删除，修改为如下的样子：

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182704558.png)手动处理冲突

手动处理以后，需要调用`git add `文件名来标识冲突已解决。然后调用`git commit -m`提交一次即可完成合并。

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182713469.png)使用git status查看发生冲突的文件

![img](https://my-wp.oss-cn-beijing.aliyuncs.com/wp-content/uploads/2022/05/20220514182722592.png)解决冲突后调用add和commit完成合并





# Vue课程

## 第一部分 预备知识 —— git

1. 安装（略）

2. 配置

   1. 配置name和email

      ``` bash
      git config --global user.name "xxxx"
      git config --global user.email "xxx@xxx.xxx"
      ```

3. 使用git：

   - 查看当前仓库的状态

     ```bash
     git status
     ```

   - 初始化仓库

     ```bash
     git init
     ```

   - 文件状态：

     1. 未跟踪
     2. 已跟踪
     3. 暂存
     4. 未修改
     5. 已修改

   - 未跟踪 → 暂存

     ```bash
     git add <filename> 将文件切换到暂存的状态
     git add * 将所有已修改（未跟踪）的文件暂存
     ```

   - 暂存 → 未修改

     ```bash
     git commit -m "xxxx" 将暂存的文件存储到仓库中
     git commit -a -m "xxxx" 提交所有已修改的文件（未跟踪的文件不会提交）
     ```

   - 未修改 → 修改

     - 修改代码后，文件会变为修改状态

4. 常用的命令

   1. 重置文件

   ```bash
   git restore <filename> # 恢复文件
   git restore --staged <filename> # 取消暂存状态
   ```

   2. 删除文件	

   ```bash
   git rm <filename> # 删除文件
   git rm <filename> -f # 强制删除
   ```

   3. 移动文件

   ```bash
   git mv from to # 移动文件 重命名文件
   ```

   ### 分支

   git在存储文件时，每一次代码代码的提交都会创建一个与之对应的节点，git就是通过一个一个的节点来记录代码的状态的。节点会构成一个树状结构，树状结构就意味着这个树会存在分支，默认情况下仓库只有一个分支，命名为master。在使用git时，可以创建多个分支，分支与分支之间相互独立，在一个分支上修改代码不会影响其他的分支。

   ```bash
   git branch # 查看当前分支
   git branch <branch name> # 创建新的分支
   git branch -d <branch name> # 删除分支
   git switch <branch name> # 切换分支
   git switch -c <branch name> # 创建并切换分支
   git merge <branch name> # 和并分支
   
   ```

   在开发中，都是在自己的分支上编写代码，代码编写完成后，在将自己的分支合并到主分支中。

   ### 变基（rebase）

   在开发中除了通过merge来合并分支外，还可以通过变基来完成分支的合并。

   我们通过merge合并分支时，在提交记录中会将所有的分支创建和分支合并的过程全部都显示出来，这样当项目比较复杂，开发过程比较波折时，我必须要反复的创建、合并、删除分支。这样一来将会使得我们代码的提交记录变得极为混乱。

   原理（变基时发生了什么）：

   1. 当我们发起变基时，git会首先找到两条分支的最近的共同祖先
   2. 对比当前分支相对于祖先的历史提交，并且将它们提取出来存储到一个临时文件中
   3. 将当前部分指向目标的基底
   4. 以当前基底开始，重新执行历史操作

   变基和merge对于合并分支来说最终的结果是一样的！但是变基会使得代码的提交记录更整洁更清晰！注意！大部分情况下合并和变基是可以互换的，但是如果分支已经提交给了远程仓库，那么这时尽量不要变基。

   ### 远程仓库（remote）

   目前我对于git所有操作都是在本地进行的。在开发中显然不能这样的，这时我们就需要一个远程的git仓库。远程的git仓库和本地的本质没有什么区别，不同点在于远程的仓库可以被多人同时访问使用，方便我们协同开发。在实际工作中，git的服务器通常由公司搭建内部使用或是购买一些公共的私有git服务器。我们学习阶段，直接使用一些开放的公共git仓库。目前我们常用的库有两个：GitHub和Gitee（码云）

   将本地库上传git：

   ```bash
   git remote add origin https://github.com/lilichao/git-demo.git
   # git remote add <remote name> <url>
   
   git branch -M main
   # 修改分支的名字的为main
   
   git push -u origin main
   # git push 将代码上传服务器上
   ```

   将本地库上传gitee：

   ```bash
   git remote add gitee https://gitee.com/ymhold/vue-course.git
   git push -u gitee main
   ```

   ### 远程库的操作的命令

   ```bash
   git remote # 列出当前的关联的远程库
   git remote add <远程库名> <url> # 关联远程仓库
   git remote remove <远程库名>  # 删除远程库
   git push -u <远程库名> <分支名> # 向远程库推送代码，并和当前分支关联
   git push <远程库> <本地分支>:<远程分支>
   git clone <url> # 从远程库下载代码
   
   git push # 如果本地的版本低于远程库，push默认是推不上去
   git fetch # 要想推送成功，必须先确保本地库和远程库的版本一致，fetch它会从远程仓库下载所有代码，但是它不会将代码和当前分支自动合并
   		 # 使用fetch拉取代码后，必须要手动对代码进行合并	
   git pull  # 从服务器上拉取代码并自动合并 
   
   ```

   注意：推送代码之前，一定要先从远程库中拉取最新的代码

      ### 		tag 标签

- 当头指针没有执行某个分支的头部时，这种状态我们称为分离头指针（HEAD detached），分离头指针的状态下也可以操作操作代码，但是这些操作不会出现在任何的分支上，所以注意不要再分离头指针的状态下来操作仓库。

- 如果非得要回到后边的节点对代码进行操作，则可以选择创建分支后再操作

  ```bash
  git switch -c <分支名> <提交id>
  ```

- 可以为提交记录设置标签，设置标签以后，可以通过标签快速的识别出不同的开发节点：

  ```bash
  git tag
  git tag 版本
  git tag 版本 提交id
  git push 远程仓库 标签名
  git push 远程仓库 --tags
  git tag -d 标签名 # 删除标签
  git push 远程仓库 --delete 标签名 # 删除远程标签
  ```

  ### gitignore

- 默认情况下，git会监视项目中所有内容，但是有些内容比如node_modules目录中的内容，我们不希望它被git所管理。我们可以在项目目录中添加一个`.gitignore`文件，来设置那些需要git忽略的文件。

### 	github的静态页面

- 在github中，可以将自己的静态页面之间部署到github中，它会给我们提供一个地址使得我们的页面变成一个真正的网站，可以供用户访问。
- 要求：
  - 静态页面的分支必须叫做：gh-pages
  - 如果希望页面可以通过xxx.github.io访问，则需要将库的名字配置为xxx.github.io 

### 	docusaurus

- facebook推出的开源的静态的内容管理系统，通过它可以快速的部署一个静态网站

- 使用：

  - 网址：

    - https://docusaurus.io/

  - 安装

    - `npx create-docusaurus@latest my-website classic`

  - 启动项目

    - `npm start`或`yarn start`

  - 构建项目

    - `npm run build`或`yarn build`
    - 

  - 配置项目：

    - docusaurus.config.js 项目的配置文件

  - 添加页面：

    - 在docusaurus框架中，页面分成三种：1.page，2.blog，3.doc

  - 案例地址：

    - https://github.com/lilichao/lilichao.github.io

    

## 第二部分 预备知识 —— 构建工具

- 当我们习惯了在node中编写代码的方式后，在回到前端编写html、css、js这些东西会感觉到各种的不便。比如：不能放心的使用模块化规范（浏览器兼容性问题）、即使可以使用模块化规范也会面临模块过多时的加载问题。
- 我们就迫切的希望有一款工具可以对代码进行打包，将多个模块打包成一个文件。这样一来即解决了兼容性问题，又解决了模块过多的问题。
- 构建工具就起到这样一个作用，通过构建工具可以将使用ESM规范编写的代码转换为旧的JS语法，这样可以使得所有的浏览器都可以支持代码。

### Webpack

- 使用步骤：

  1. 初始化项目`yarn init -y`
  2. 安装依赖`webpack`、`webpack-cli`
  3. 在项目中创建`src`目录，然后编写代码（index.js）
  4. 执行`yarn webpack`来对代码进行打包（打包后观察dist目录）

- 配置文件（webpack.config.js）

  ```javascript
  const path = require("path")
  module.exports = {
      mode: "production", 
      entry: "./src/index.js",
      output: {
      }, 
      module: {
          rules: [
              {
                  test: /\.css$/i,
                  use: ["style-loader", "css-loader"]
              }
          ]
      }
  }
  
  ```

- 在编写js代码时，经常需要使用一些js中的新特性，而新特性在旧的浏览器中兼容性并不好。此时就导致我们无法使用一些新的特性。

- 但是我们现在希望能够使用新的特性，我们可以采用折中的方案。依然使用新特性编写代码，但是代码编写完成时我们可以通过一些工具将新代码转换为旧代码。

- babel就是这样一个工具，可以将新的js语法转换为旧的js，以提高代码的兼容性。

- 我们如果希望在webpack支持babel，则需要向webpack中引入babel的loader

- 使用步骤

  1. 安装 `npm install -D babel-loader @babel/core @babel/preset-env`

  2. 配置：

     ```javascript
     module: {
       rules: [
         {
           test: /\.m?js$/,
           exclude: /(node_modules|bower_components)/,
           use: {
             loader: 'babel-loader',
             options: {
               presets: ['@babel/preset-env']
             }
           }
         }
       ]
     }
     ```

  3. 在package.json中设置兼容列表

     ```json
     "browserslist": [
             "defaults"
      ]
     ```

     https://github.com/browserslist/browserslist

- 插件（plugin）

  - 插件用来为webpack来扩展功能

  - html-webpack-plugin

    - 这个插件可以在打包代码后，自动在打包目录生成html页面

    - 使用步骤：

      1. 安装依赖
      2. 配置插件

      ```javascript
      plugins: [
              new HTMLPlugin({
                  // title: "Hello Webpack",
                  template: "./src/index.html"
              })
          ]
      ```

- 开发服务器（webpack-dev-server）

  - 安装：
    - `yarn add  -D webpack-dev-server`
    - 启动：`yarn webpack serve --open`

- `devtool:"inline-source-map"`配置源码的映射

## Vite

- Vite也是前端的构建工具

- 相较于webpack，vite采用了不同的运行方式：

  - 开发时，并不对代码打包，而是直接采用ESM的方式来运行项目
  - 在项目部署时，在对项目进行打包

- 除了速度外，vite使用起来也更加方便

- 基本使用：

  1. 安装开发依赖 vite

  2. vite的源码目录就是项目根目录

  3. 开发命令：

     vite 启动开发服务器

     vite build 打包代码

     vite preview 预览打包后代码

- 使用命令构建

  ```bash
  npm create vite@latest
  yarn create vite
  pnpm create vite
  ```

- 配置文件：`vite.config.js`

- 格式：

  ```javascript
  import { defineConfig } from "vite"
  import legacy from "@vitejs/plugin-legacy"
  
  export default defineConfig({
      plugins: [
          legacy({
              targets: ["defaults"]
          })
      ]
  })
  ```

  

## 第三部分 Vue

### vue

- vue是一个前端的框架，主要负责帮助我们构建用户的界面
- MVVM：Model - View - View Model
- vue负责vm的工作（视图模型），通过vue可以将视图和模型相关联。
  - 当模型发生变化时，视图会自动更新
  - 也可以通过视图去操作模型
- vue思想：
  - 组件化开发
  - 声明式的编程

### HelloWorld

1. 直接在网页中使用（像jQuery一样）

   - `        <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>`

2. 使用vite

   - `yarn add vite -D`

3. 代码：

   ```javascript
   // 组件，就是一个普通js对象
   const App = {}
   
   // 创建应用
   const app = createApp(App)
   
   // 挂载到页面
   app.mount("#root")
   ```

4. 自动创建项目

   - `npm init vue@latest`
   - `yarn create vue`



## 网页的渲染

- 浏览器在渲染页面时，做了那些事：

  1. 加载页面的html和css（源码）
  2. html转换为DOM，css转换为CSSOM
  3. 将DOM和CSSOM构建成一课渲染树
  4. 对渲染树进行reflow（回流、重排）（计算元素的位置）
  5. 对网页进行绘制repaint（重绘）

- 渲染树（Render Tree）

  - 从根元素开始检查那些元素可见，以及他们的样式
  - 忽略那些不可见的元素（display:none）

- 重排、回流

  - 计算渲染树中元素的大小和位置
  - 当页面中的元素的大小或位置发生变化时，便会触发页面的重排（回流）
  - width、height、margin、font-size ......
  - 注意：每次修改这类样式都会触发一次重排！所以如果分词修改多个样式会触发重排多次，而重排是非常耗费系统资源的操作（昂贵），重排次数过多后，会导致网页的显示性能变差，在开发时我们应该尽量的减少重排的次数
  - 在现代的前端框架中，这些东西都已经被框架优化过了！所以使用vue、react这些框架这些框架开发时，几乎不需要考虑这些问题，唯独需要注意的时，尽量减少在框架中直接操作DOM

- 重绘

  - 绘制页面
  - 当页面发生变化时，浏览器就会对页面进行重新的绘制

- 例子：

  ```html
  <!DOCTYPE html>
  <html lang="zh">
      <head>
          <meta charset="UTF-8" />
          <meta http-equiv="X-UA-Compatible" content="IE=edge" />
          <meta name="viewport" content="width=device-width, initial-scale=1.0" />
          <title>Document</title>
          <style>
              .box1 {
                  width: 200px;
                  height: 200px;
                  background-color: orange;
              }
  
              .box2 {
                  background-color: tomato;
              }
  
              .box3 {
                  width: 300px;
                  height: 400px;
                  font-size: 20px;
              }
          </style>
      </head>
      <body>
          <button id="btn">点我一下</button>
          <hr />
          <div id="box1" class="box1"></div>
          <script>
              btn.onclick = () => {
                  // box1.classList.add("box2")
                  // 可以通过修改class来间接的影响样式，来减少重排的次数
                  // box1.style.width = "300px"
                  // box1.style.height = "400px"
                  // box1.style.fontSize = "20px"
                  // box1.classList.add("box3")
                  // box1.style.display = "none"
                  // box1.style.width = "300px"
                  // box1.style.height = "400px"
                  // box1.style.fontSize = "20px"
                  // div.style.display = "block"
              }
          </script>
      </body>
  </html>
  
  ```

  

