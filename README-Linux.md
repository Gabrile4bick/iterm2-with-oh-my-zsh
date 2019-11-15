# Linux 无root权限安装zsh和oh-my-zsh

## 1. 下载安装zsh
查看zsh最新版本：[zsh](http://zsh.sourceforge.net/Arc/source.html)

#### 下载
```
cd ~/soft # or any directory of your choice
wget https://sourceforge.net/projects/zsh/files/zsh/5.7.1/zsh-5.7.1.tar.xz
```
#### 解压
```
tar xvJf zsh-5.7.1.tar.xz
```
#### 编译
```
cd zsh-5.7.1
./configure --prefix=$HOME
make
make install
```
注意：这里可以先创建一个目录```mkdir ~/zsh```，把$HOME替换为```~/zsh```

## 2. 更新PATH（环境变量）
zsh 安装到 $HOME/bin 下面，并且会自动添加环境变量，但是重新登陆后就找不到了。所以要手动更新 PATH ，将下面命令写入 ~/.bash_profile 文件。
```
echo 'export PATH="$HOME/bin:$HOME/.local/bin:$PATH"' >> ~/.bash_profile
```
这样操作之后就可以在命令行使用 zsh 了，但是不会默认使用 zsh 作为交互程序。修改启动脚本，自动切换到 zsh （官方推荐的方式），将下面命令写入 ~/.bash_profile文件：
```
echo '[ -f $HOME/bin/zsh ] && exec $HOME/bin/zsh -l' >> ~/.bash_profile
```
加载环境配置并执行zsh交互方式：
```
source ~/.bash_profile
```

## 3. 安装oh-my-zsh
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
退出重新登录

打开zsh配置文件
```
vi .zshrc
```
从该文件中找到下面的命令行，按i进入编辑模式，去掉开头的#，取消该行注释:
```
export PATH=$HOME/bin:/usr/local/bin:$PATH
```
按esc退出vi编辑模式，输入:wq保存并退出vi模式。

