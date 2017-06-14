
## ディレクトリにファイル数を数える

```
ls -1 | wc -l
```

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

## tar/zipコマンドで解凍・圧縮一覧まとめ（gz、zip、tar.xzなど）

http://uguisu.skr.jp/Windows/tar.html

## sshポートフォワーディング

```
ssh -L port:target:hostport [user@]hostname
```

```
ssh -L 80:target:8080 [user@]hostname
local(80) --ssh--> hostname --> (8080)target
```


