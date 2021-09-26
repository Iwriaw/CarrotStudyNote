# Mac OS 使用笔记
## 设置python3为默认python
在~/.bash_profile中输入：
```sh
export PATH=${PATH}:/usr/local/bin/python3
alias python="/usr/local/bin/python3"
```
然后在终端输入source ~/.bash_profile

此时再输入python，默认启动了python3即为成功。

重新打开又恢复为原来的设置了？

在.zshrc中输入
```sh
source ~/.bash_profile
```
因为zsh的启动的环境变量不是.bash_profile，而是.zshrc。