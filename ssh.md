#生成 rsa key 

```
ssh-keygen -t rsa -b 2048
```

#将ssh key添加到其他机器的信任列表中

```
ssh-copy-id [username@]hosntame
```
例如:
```
ssh-copy-id localhost
```

添加好后可以验证一下
```
ssh localhost "cat .ssh/authorized_keys"
```

#将ssh key添加到github

在[设置页面](https://github.com/settings/ssh)操作

验证使用
```
ssh -T git@github.com
```
随后就可以使用ssh 访问github 上的repository, 例如:
```
git clone git@github.com:liangguo/mydebenv.git
```
每个git repository的地址可以在repository的右下方找到, 默认是https, 点ssh后出现可
以使用ssh访问的地址.

#将ssh key 上传到debian.org
Debian.org管理的机器都不允许使用密码登陆, 所以需要将ssh key添加到debian.org的数据
库中, 标准的方式是使用mail程序通过[LDAP Gateway](https://db.debian.org/doc-mail.html)
进行修改, 命令如下:
```
cat .ssh/id_rsa.pub | gpg --clearsign | mail changes@db.debian.org
```
但是这样修改需要配置mail能发送邮件到外网, 比较麻烦. 如果可以访问debian.org的机器,
比如alioth.d.o, 则可以在该机器执行发邮件的操作. 具体步骤如下:

```
cat .ssh/authorized_keys |gpg --clearsign >sshkey
scp sshkey alioth.debian.org:./
ssh alioth.debian.org "cat sshkey|mail changes@db.debian.org"
```

因为需要将多个ssh key 上传到debian.org, 所以我使用了`.ssh/authorized_keys`, 而不
是`.ssh/id_rsa.pub`. 

从发邮件到生效可能需要1小时或更多的时间. 

登陆alioth的ssh key可以在[这个页面](https://alioth.debian.org/account/editsshkeys.php)`. 

从发邮件到生效可能需要1小时或更多的时间. 

登陆alioth.d.o的ssh key可以在[这个页面](https://alioth.debian.org/account/editsshkeys.php)
进行编辑, 更多信息请参考[alioth.d.o的Wiki](https://wiki.debian.org/Alioth/SSH)
进行编辑, 更多信息请参考[alioth.d.o的Wiki](https://wiki.debian.org/Alioth/SSH)
