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
注意：这里在主目录`~`下面会生成三个新的目录`bin`，`lib`，`share`，可以先创建一个目录`mkdir ~/zsh`，把$HOME替换为`~/zsh`

## 2. 更新PATH（环境变量）
zsh 安装到 $HOME/bin 下面，并且会自动添加环境变量，但是重新登陆后就找不到了。所以要手动更新 PATH ，将下面命令写入 ~/.bash_profile 文件。
```
echo 'export PATH="$HOME/bin:$HOME/.local/bin:$PATH"' >> ~/.bash_profile
```
这样操作之后就可以在命令行使用 zsh 了，但是不会默认使用 zsh 作为交互程序。修改启动脚本，自动切换到 zsh （官方推荐的方式），将下面命令写入 ~/.bash_profile文件：
```
echo '[ -f $HOME/bin/zsh ] && exec $HOME/bin/zsh -l' >> ~/.bash_profile
```
加载环境配置并运行zsh交互方式(或者退出重新登录)：
```
source ~/.bash_profile
```

## 3. 安装oh-my-zsh
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
打开zsh配置文件
```
vi .zshrc
```
从该文件中找到下面的命令行，按i进入编辑模式，去掉开头的#，取消该行注释:
```
export PATH=$HOME/bin:/usr/local/bin:$PATH
```
按esc退出vi编辑模式，输入:wq保存并退出vi模式。

加载环境配置并运行oh-my-zsh（或者退出重新登录）：
```
source .zshrc
```
由于zsh⾥的vi打开文件无高亮显示，和vim有区别，我们用alias命令将vi替换成vim
```
alias vi='vim'
```
这样vi打开文件就有高亮显示了


## 4. 主题修改与插件配置

#### 主题修改
```
vi .zshrc
```
找到ZSH_THEME并修改为`agnoster`或者`ys`
```
ZSH_THEME="ys"
```
主题存放位置~/.oh-my-zsh/themes，可以进行选择

#### 插件配置
**1) zsh-autosuggestions：自动补全**
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
**2) zsh-syntax-highlighting：语法高亮**
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
这时我们需要再次打开.zshrc文件进行编辑
```
vi .zshrc
```
找到plugins，此时plugins中应该已经有了git，我们需要把自动补全、语法高亮插件也加上，请务必保证插件顺序，zsh-syntax-highlighting必须在最后一个。

```
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
 )
```
然后在文件的最后添加：

source ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh

source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

按esc退出vi编辑模式，输入:wq保存并退出vi。

执行下面命令使刚才的修改生效(或者退出重新登录)：
```
source .zshrc
```

**3) [autojump](https://github.com/wting/autojump)：快速跳转**

下载：
```
git clone git://github.com/wting/autojump.git
```
安装：
```
cd autojump
./install.py
```
最后把以下代码加入.zshrc：
```
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && source ~/.autojump/etc/profile.d/autojump.sh
```

**4) [z](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/z)：目录间快速跳转**

参考：
https://www.zcfy.cc/article/become-a-command-line-power-user-with-oh-my-zsh-and-z-920.html
