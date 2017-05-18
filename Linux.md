## IPに名前をつける

```
$ vi .ssh/config
Host foo
  HostName xxx.xxx.xxx.xxx
HOST bar
  HostName xxx.xxx.xxx.xxx
  
$ chmod 600 .ssh/config 
```

## 公開鍵と秘密鍵を作成する
```
$ ssh-keygen -t rsa
```

## 公開鍵をクライアントに設置する
```
$ ssh-copy-id xxx.xxx.xxx.xxx
```
