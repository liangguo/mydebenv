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

