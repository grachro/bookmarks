
## 事前準備

### VirtualBoxのインストール
- VirtualBox https://www.virtualbox.org/

インストールが終わったら起動してください。

### Vagrantのインストール
- Vagrant https://www.vagrantup.com/

インストールが終わったらvagrantコマンドが使えるようになります。
```
$ vagrant --version
Vagrant 1.9.4
```

## Vagrantプロジェクトの初期化からVM起動まで

適当な場所に作業ディレクトリを作成。場所と名前はどこでも可です。以下の説明は適当に読み替えてください。
今回の説明では、VMのOSにCentOS7を使います。他のOSを使う場合は[ここ](https://atlas.hashicorp.com/boxes/search)で探して下さい。

```
$ mkdir -p /your/directory/centos7
$ cd /your/directory/centos7
```

initコマンドで初期化します。Vagrantfileが作成されます。
```
$ vagrant init centos/7
```

VirtualBoxにVMを起動
```
$ vagrant up
```

無事立ち上がったら、VMにvagrant sshでログインできます
```
$ vagrant ssh
```

## Vagrantで立ち上げたVMに、普通のsshでログイン

### ディフォルト設定でsshログイン

SSH接続情報を確認
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

ディフォルトでは、ホストOSのポート2222に、VMのポート22がフォワードされています。

```
$ ssh -i /your/directory/centos7/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@127.0.0.1
とか
$ ssh -i /your/directory/centos7/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@localhost

...
Are you sure you want to continue connecting (yes/no)? yes
[vagrant@localhost ~]$ 
```




## VirtualBoxのVMを停止・削除

```
$ vagrant destroy
```
