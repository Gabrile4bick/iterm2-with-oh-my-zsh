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
