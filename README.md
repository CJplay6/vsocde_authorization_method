# vsocde_authorization_method

## 服务端配置

1. 检查windows中是否安装ssh(在cmd命令窗口中输入ssh)
2. 生成id_rsa.pbu(ssh-keygen -t rsa)
3. 将C://Users/xxx/.ssh/id_rsa.pub拷贝到服务器的~/.ssh/authorized_keys，请不要采用复制粘贴文本的方式，我是用xftp将文件复制到服务器，再执行如下命令：
```
cat id_rsa.pub >> authorized_keys
```
4. 修改/etc/ssh/sshd_config:
```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile ~/.ssh/authorized_keys
```
5. 重启ssh
```
service sshd restart
```
6. 在CMD中ssh name@x.x.x.x (name为服务器登录名），如果没有提示输入密码，则配置成功

##以上操作都完成后还是不行可以尝试修改文件权限如下##

```
sudo chmod 600 authorized_keys
sudo chmod 700 ~/.ssh
```
7. 如果在保证配置免密成功的前提下，希望关闭密码登录，可以修改/etc/ssh/sshd_config：PasswordAuthentication no （ 谨慎操作，免密登录配置失败的话就和服务器说再见了。。）再重启sshd服务
