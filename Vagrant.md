## プロジェクトディレクトリを作成

```
$ mkdir -p /your/directory/centos7
$ cd /your/directory/centos7
```
ディレクトリの場所と名前はどこでも可


## Vagrantプロジェクトを初期化

```
$ vagrant init centos/7
```
Vagrantfileが作られる。

Vagrantfileのネットワークを適当なものに変更
```
# config.vm.network "private_network", ip: "192.168.xx.xx"
config.vm.network "private_network", ip: "192.168.xx.xx"
```


## VirtualBoxにVMを起動

```
$ vagrant up
```
初回は時間がかかる

## VMにvagrant sshでログイン

```
$ vagrant ssh
```

## VMに普通のsshでログイン

### SSH接続情報を確認
```
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /your/directory/centos7/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

### 接続
```
$ ssh -i /your/directory/centos7/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@127.0.0.1
...
Are you sure you want to continue connecting (yes/no)? yes
[vagrant@localhost ~]$ 
```




## VirtualBoxのVMを停止・削除

```
$ vagrant destroy
```
