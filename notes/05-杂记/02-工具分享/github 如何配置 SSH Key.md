# github 如何配置 SSH Key

## 一、安装

### 1）下载

```
下载地址：https://git-scm.com/downloads
```



## 二、配置

### 1）生成ssh key

生成ssh key之前先检查本地主机是否已经存在ssh key，检查 “~/.ssh” 目录下是否存在 **id_rsa** 和 **id_rsa.pub** 文件，如果存在，说明已经有 ssh Key。

安装git软件后，右键-> Git Bush。 如果没有则使用下面命令生成 ssh key。

```bash
$ ssh-keygen -t rsa -C "your_email@example.com"
```

### 2）添加ssh key到 Github

登录 Github -> 右上角图标 -> Settings -> SSH and GPG keys -> New SSH key -> Title 随便填写 -> Key 复制 id_rsa.pub 文件内容粘贴到 Key 中 -> Add SSH key

### 3）测试ssh key是否配置成功

```bash
$ ssh -T git@github.com
```



## 三、原理

SSH登录安全性由非对称加密保证，产生密钥时，一次产生两个密钥。一个公钥，一个私钥，在git中一般命名为id_rsa.pub, id_rsa。

那么如何使用生成的一个私钥一个公钥进行验证呢？

- 公钥认证流程：

  1. Client端用户1将自己的公钥存放在Server上，追加在文件authorized_keys中。

  2. Server收到登录请求后，随机生成一个字符串A，并发送给Client。

  3. Client用自己的私钥对字符串A进行加密。

  4. 将加密后字符串发送给Server。

  5. Server用之前存储的公钥进行解密，比较解密后的A和B。

  6. 根据比较结果，返回客户端登陆结果。


![img](./images/202503111637.png)