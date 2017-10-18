# 多个SSH Key

## Key生成

```
ssh-keygen -t rsa -b 4096 -C "mobai@tsign.cn"
Enter file in which to save the key (/Users/zhouleibo/.ssh/id_rsa): id_rsa_tsign
```

## 新建config文件

```
Host code.tsign.cn
  HostName code.tsign.cn
  User mobai
  IdentityFile /Users/zhouleibo/.ssh/id_rsa_tsign
```