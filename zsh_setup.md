# zsh 搭建安装

1. 检查shell安装情况：
```shell
cat /etc/shells
```

2. 如果没有/bin/zsh，安装zsh：
```shell
sudo apt install zsh

chsh -s /bin/zsh  #将zsh设置成默认shell
```

3. 使用oh-my-zsh搭建zsh配置， 安装方式：
```shell
sh -c "$(curl -fsSL https://gitee.com/shmhlsy/oh-my-zsh-install.sh/raw/master/install.sh)" #国内镜像源
```
  如果安装成功则会出现彩色oh my zsh的figlet斜体

  figlet字体： 
```shell
sudo apt install figlet #下载figlet命令行
figlet oh my zsh #这里不是斜体的，但大概就长这种形式
```

4. 下载必备二件套

  - zsh-autosuggestions 根据命令行历史输入自动提示， 按➡️ （键盘右下角上下左右的那个右）自动补全

    注意只有已经键入过的命令才会自动补全，和tab补全不太一样，但会把补全内容显示出来，非常好用
  - zsh-syntax-highlighting 语法提示，输入正确的命令语法会是绿色，错误的则是红色

    e.g. touch main.cpp 中touch会是绿色的，touchh main.cpp 中touchh则是红色的

  下载方式：
  ```shell
  # zsh-autosuggestions
  git clone https://gitee.com/kanderWall/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  # zsh-syntax-highlighting
  git clone https://gitee.com/Annihilater/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```

  然后在 ~/.zshrc中的插件处修改如下：
  ```shell
  # 打开~/.zshrc文件， 这个文件可以理解成启动shell的时候会执行这个文件
  vim ~/.zshrc #或者
  nano ~/.zshrc #就用喜欢的文本编辑器打开就行
  ```

  找到这样的一块内容：
  ```
  plugins=(
    ...
  )
  ```
  将其修改为
  ```
  plugins=(
    ...
    zsh-autosuggestions
    zsh-syntax-highlighting
    ...
  )

  比如我的就是：
  plugins=(
	  git
	  z
	  zsh-autosuggestions
	  zsh-syntax-highlighting
	  fzf
      you-should-use
  )
  ```

5. 其它一些小插件推荐：
  - z 目录自动跳转， 可以记住你到过的文件夹，然后你输入一个文件夹名的一部分就可以快速跳转了

    举个例子：
    ```shell
    # 我现在在不知道什么地方， 想要去 ～/Desktop/大学/大二-秋/280/Projects/P3 这个地方
    z P3
    # 这就到了，甚至不区分大小写，不完整字符串也能识别。比如我经常去 ~/Desktop/大学/大二-秋/280/Projects/P3/Project-3-Related-Files/tests 只需要输入
    z te
    # 就可以到达了
    ```

    这个我还真忘了怎么装的了，我不知道是不是ohmyzsh自带的，加进plugins括号就能用了

  - you-should-use 有时候alias设置太多了自己记不清，它可以告诉你你可以使用的alias

    安装：
    ```shell
    git clone https://gitee.com/yorelog/zsh-you-should-use.git $ZSH_CUSTOM/plugins/you-should-use
    ```

    同样地，加入plugins的括号就可以用了, 就像我上面一样

  - fzf 模糊查找，这个我不常用，但挺多人都挺喜欢的

    安装：
    ```shell
    sudo apt install fzf
    ```

    至于用法, 我就只有这些，可以多看看官方教学或者别人的视频，b站有个up叫theCW好像有一期视频讲这个的：

    ```shell
    Command-line fuzzy finder.
    Similar to `sk`.
    More information: <https://github.com/junegunn/fzf>.

    - Start `fzf` on all files in the specified directory:
    find path/to/directory -type f | fzf

    - Start `fzf` for running processes:
    ps aux | fzf

    - Select multiple files with `Shift + Tab` and write to a file:
    find path/to/directory -type f | fzf --multi > path/to/file

    - Start `fzf` with a specified query:
    fzf --query "query"

    - Start `fzf` on entries that start with core and end with either go, rb, or py:
    fzf --query "^core go$ | rb$ | py$"

    - Start `fzf` on entries that not match pyc and match exactly travis:
    fzf --query "!pyc 'travis"
    ```