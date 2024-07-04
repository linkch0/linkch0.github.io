---
icon: material/console
tags: [Updating]
comments: true
---

# Command Lines

## Linux :simple-linux:

1. 获取当前`bash pid`：`ps -p $$`，获取`fish-shell pid`: `ps -p $fish_pid`
2. Commands for Manipulating The History
    -   <https://www.gnu.org/software/bash/manual/html_node/Commands-For-History.html>
    -   reverse-search-history (C-r)
3. Read from standard input and write to standard output and files
    -   `echo "example" | tee path/to/file`

## ZSH

Environment: No Internet, no `sudo` root privilege.

Install ZSH under user directory. Download ZSH source code: <https://sourceforge.net/projects/zsh/>

1. Extract

    ```shell
    xz -d zsh-5.9.tar.xz
    tar -xf zsh-5.9.tar
    cd zsh-5.9
    ```

2. Compile ZSH

    ```shell
    ./configure --prefix=/home/chenlu/.local/lib/zsh-5.9
    make
    make install
    ```

3. Create soft link

    ```shell
    ln -s ~/.local/lib/zsh-5.9/bin/zsh ~/.local/bin/zsh
    ```

Install oh-my-zsh. Download oh-my-zsh source code: <https://github.com/ohmyzsh/ohmyzsh>

You can create a new zsh config file by copying the template that we have included for you.

```shell
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

Install powerlevel10k. <https://github.com/romkatv/powerlevel10k#how-do-i-install-powerlevel10k-on-a-machine-without-internet-access>

1.  Run this command on the machine without Internet access:

    ```shell
    uname -sm | tr '[A-Z]' '[a-z]'
    ```

2.  Run these commands on a machine connected to the Internet after replacing the value of `target_uname` with the output of the previous command:

    ```shell
    target_uname="replace this with the output of the previous command"
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
    GITSTATUS_CACHE_DIR="$HOME"/powerlevel10k/gitstatus/usrbin ~/powerlevel10k/gitstatus/install -f -s "${target_uname% *}" -m "${target_uname#* }"
    ```

3.  Copy `~/powerlevel10k` from the machine connected to the Internet to the one without Internet access.

4.  Add `source ~/powerlevel10k/powerlevel10k.zsh-theme` to `~/.zshrc` on the machine without Internet access:

    ```shell
    echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
    ```

5.  If `~/.zshrc` on the machine without Internet access sets `ZSH_THEME`, remove that line.

    ```shell
    sed -i.bak '/^ZSH_THEME=/d' ~/.zshrc
    ```

To update, remove `~/powerlevel10k` on both machines and repeat steps 1-3.

```shell
mv ~/powerlevel10k ~/.oh-my-zsh/custom/themes/
ZSH_THEME="powerlevel10k/powerlevel10k"
```

## GDB :simple-gnu:

GNU is a recursive acronym for "GNU's Not Unix!".

`gcc`: GNU project C and C++ compiler

`gdb`: The GNU Debugger

使用`gdb`之前，通常使用`gcc -g test.c`编译文件，`man gcc`

```
-g  Produce debugging information in the operating system's native format (stabs, COFF, XCOFF, or DWARF).  GDB can work with this
           debugging information.

           On most systems that use stabs format, -g enables use of extra debugging information that only GDB can use; this extra information
           makes debugging work better in GDB but probably makes other debuggers crash or refuse to read the program.  If you want to control
           for certain whether to generate the extra information, use -gstabs+, -gstabs, -gxcoff+, -gxcoff, or -gvms (see below).
```

`gdb`中回车会默认执行上一次命令

1. `help`

    ```
    Type "help" followed by a class name for a list of commands in that class.
    Type "help all" for the list of all commands.
    Type "help" followed by command name for full documentation.
    ```

2. `file`: Use FILE as program to be debugged. It is read for its symbols, for getting the contents of pure memory.

3. `list` or `l`: List specified function or line. With no argument, lists ten more lines after or around previous listing.

4. `run` or `r`: Start debugged program. You may specify arguments to give it.

5. `start`: Start the debugged program stopping at the beginning of the main procedure.

6. `next` or `n`: Step over. Step program, proceeding through subroutine calls.

7. `step` or `s`: Step into. Step program until it reaches a different source line.

8. `finish`: Step out. Execute until selected stack frame returns.

9. `print` or `p`: Print value of expression EXP.

10. `break` or `b`: Set breakpoint at specified location.

11. `info` or `i`: Generic command for showing things about the program being debugged.

12. `info break` or `i b`: Status of specified breakpoints.

13. `delete` or `d`: Delete all or some breakpoints.

## Git :simple-git:

[官方文档](https://git-scm.com/docs)，[菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

-   working directory 工作区
-   staging area 暂存区
-   repository 版本库

<!-- more -->

![staging area](https://git-scm.com/images/about/index1@2x.png)

### 创建仓库

1. `git init` 当前目录
2. `git init dir` 指定目录

### 克隆仓库

1. `git clone url` 默认目录名为仓库名
2. `git clone url dir` 克隆到指定目录
3. `git clone -b branchname url` 克隆指定分支，没有`-b`默认克隆 master 分支

### 设置提交代码时的用户信息

1. `git config --global user.name "username"` 用户名
2. `git config --global user.email email@xxx.com` 邮箱

### 分支管理

1. `git branch` 列出分支
2. `git branch branchname` 创建分支
3. `git branch -d branchname` 删除分支
4. `git checkout branchname` 切换指定分支
5. `git checkout -b branchname` 创新分支并立即切换
6. `git merge branchname` 合并分支到当前分支

### 提交与修改

1. `git status` 查看当前的状态，显示有变更的文件
2. `git status -s` 简短输出
3. `git diff` 比较文件的不同，即暂存区和工作区的差异
4. `git diff filename` 指定文件
5. `git log` 查看提交历史
6. `git log --online` 简短输出
7. `git blame filename` 以列表形式查看指定文件的历史修改记录
8. `git add .` 添加所有文件到暂存区
9. `git commit -m "message"` 将暂存区内容提交到本地仓库中
10. `git commit -am "message"` 首先 add 所有修改的文件，再提交，新创建的文件不会被添加
11. `git reset --mixed commitID` 默认回退模式，可以不填`--mixed`，回退版本库，回退暂存区，保留工作区
12. `git reset --soft commitID` 只回退版本库，commit 的信息
13. `git reset --soft commitID` 回退所有信息，工作区源码也会回退

### 远程仓库

1. `git remote` 查看远程仓库
2. `git remote -v` verbose 显示更多信息
3. `git remote show remotename` 显示指定远程仓库的信息
4. `git remote add remotename url` 添加远程仓库
5. `git push remotename` 推送当前分支到远程仓库

## FFmpeg :simple-ffmpeg:

[官方文档](https://ffmpeg.org/ffmpeg.html)

<!-- more -->

1. 查看 mkv 封装信息, `ffmpeg -i input.mkv`
2. mkv 只分离视频为 mp4, `ffmpeg -i input.mkv -vcodec copy -an output.mp4`
3. mkv 只分离音频为 flac, `ffmpeg -i input.mkv -acodec copy -vn output.flac`
4. flv 分离为 mp4, `ffmpeg -i input.flv -c copy output.mp4`
5. 提取 mp4 的音频为 mp3, `ffmpeg -i audio.mp4 -vn audio.wav/mp3`
6. 合并音频和视频文件，并使用 aac 重新编码音频文件, `ffmpeg -i video.mp4 -i audio.wav/mp3 -c:v copy -c:a aac output.mp4 `

## Fish Shell :fontawesome-solid-fish-fins:

1. Config file path `~/.config/fish/config.fish`

2. Oh my posh `oh-my-posh init fish --config ~/Documents/ohmyposh.json | source`

3. Vi mode

    ```shell
    set fish_cursor_default block
    set fish_cursor_insert underscore
    # set fish_cursor_replace_one underscore
    # set fish_cursor_visual block
    ```

4. iTerm2 shell integration `source ~/.iterm2_shell_integration.fish`

## Homebrew :simple-homebrew:

换阿里云源：<https://developer.aliyun.com/mirror/homebrew>，从阿里云下载安装脚本并安装 Homebrew 

```shell
git clone https://mirrors.aliyun.com/homebrew/install.git brew-install
/bin/bash brew-install/install.sh
rm -rf brew-install
```

-   bash

    ```shell
    echo 'export HOMEBREW_API_DOMAIN="https://mirrors.aliyun.com/homebrew-bottles/api"' >> ~/.bash_profile
    echo 'export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/brew.git"' >> ~/.bash_profile
    echo 'export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/homebrew-core.git"' >> ~/.bash_profile
    echo 'export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.aliyun.com/homebrew/homebrew-bottles"' >> ~/.bash_profile
    source ~/.bash_profile
    brew update
    ```

-   zsh

    ```shell
    echo 'export HOMEBREW_API_DOMAIN="https://mirrors.aliyun.com/homebrew-bottles/api"' >> ~/.zshrc
    echo 'export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/brew.git"' >> ~/.zshrc
    echo 'export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/homebrew-core.git"' >> ~/.zshrc
    echo 'export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.aliyun.com/homebrew/homebrew-bottles"' >> ~/.zshrc
    source ~/.zshrc
    brew update
    ```

1. Search openjdk `brew search openjdk`
2. Install openjdk `brew install openjdk`
3. List services `brew services list`
4. Start/Stop mysql service `brew services start/stop mysql`

## Docker :simple-docker:

1. Create and run a container with name "ubuntu", hostname "ubuntu", volume source "$PWD/CSAPP", destination "/CSAPP", using image ubuntu

    `docker run -it --name ubuntu --hostname ubuntu --platform linux/amd64 --volume "$PWD/CSAPP:/CSAPP" ubuntu /bin/bash`

2. See docker process `docker ps -a`

3. Container

    - list: `docker container ls`
    - remove: `docker container rm 2a56b6fa205b`
    - start: `docker start -ia ubuntu`
    - stop: `docker stop ubuntu`

4. Image

    - list: `docker image ls`
    - pull: `docker pull ubuntu:latest`
    - save: `docker save -o oracle-ee.tar repo:tag`
    - load: `docker load -i oracle-ee.tar`

## Tmux :simple-tmux:

Document: <https://github.com/tmux/tmux/wiki/Getting-Started#getting-started>

`.tmux.conf`

<script src="https://gist.github.com/linkch0/5d3c6d9a2291918f709fca753f8f939a.js"></script>

1.   The prefix key
     -   `C-b`, Control + B
     -   `C-` for the control key
     -   `M-` for the meta key (normally `Alt` on modern computers)
     -   `S-` for the shift key
2.   Help keys `C-b ?`
3.   Window operations
     -   Create `C-b c`
     -   Split horizontally `C-b s`
     -   Split vertically `C-b v`
4.   Select pane
     -   Up `C-b k`
     -   Down `C-b j`
     -   Left `C-b h`
     -   Right `C-b l`
5.   Copy mode and using vi movement `C-b [`
6.   Display pane numbers `C-b q`
7.   Kill the active pane `C-b x`
8.   Resize pane by 5
     -   Up `C-b M-Up`
     -   Down `C-b M-Down`
     -   Left `C-b M-Left`
     -   Right `C-b M-Right`
9.   Run shell commands
     -   `run` or `run-shell`
     -   e.g. `run pwd`

10.   Formats
      -   Document: <https://github.com/tmux/tmux/wiki/Formats>
      -   Display a format `tmux display -p #{}`
      -   e.g. `tmux display -p '#{pid}'`
      -   e.g. `tmux display -p '#{status-right}'`

