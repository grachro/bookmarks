
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
$ mkdir -p /your/directory/vm1
$ cd /your/directory/vm1
```

initコマンドで初期化します。Vagrantfileが作成されます。
```
$ vagrant init centos/7
```

VirtualBoxにVMを起動
```
$ vagrant up
```

無事立ち上がったら、VMにvagrant sshでログインできます。ログアウトはexitです。
```
$ vagrant ssh
```


destroyコマンドで、VirtualBoxのVMを停止・削除できます。vm内での変更は破棄されます。

```
$ vagrant destroy
```


## Vagrantで立ち上げたVMにディフォルト設定でsshでログイン

vagrant sshではなく、普通のsshでログインしてみます。

ssh-configコマンドで、SSH接続情報を確認できます。
```
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /your/directory/vm1/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

ディフォルトでは、ホストOSのport 2222に、VMのport 22がフォワードされています。このため、localhostのport 2222に対してsshでログインできます。選んだOSによってはUserがvagrant以外になっているかもしれません。

```
$ ssh -i /your/directory/vm1/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@127.0.0.1
とか
$ ssh -i /your/directory/vm1/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@localhost

[vagrant@localhost ~]$ 
```

su -でrootになる場合、パスワードはvagrantです。


## VMに接続するポートを変えてsshログイン
ディフォルトの設定のままで2台目のVMを起動させると、port 2222にフォワードしようとして失敗するため、2223を割り振ってみます。
新しい作業ディレクトリを作って、vagrant initコマンドを実行し、作成されたVagrantfileをテキストエディタで開きます。
```
$ mk /your/directory/vm2
$ cd /your/directory/vm2
$ vagrant init centos/7
$ vi Vagrantfile
```

Vagrantfileに１行追加
```
config.vm.network "forwarded_port", guest: 22, host: 2223, id: "ssh"
```


vagrant upでVMを起動して、vagrant ssh-configで接続情報を確認すると、ポートが2223に変わっています。
```
$ vagrant up
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2223
以下略
```

port 2223でsshログインできます。
```
$ ssh -i /your/directory/vm2/.vagrant/machines/default/virtualbox/private_key -p 2223 vagrant@localhost
[vagrant@xxx ~]$ 
```

## VMのipを変えてsshログイン
今度はVMにホストOSとは別の、IPアドレス割り振って、ホストOSからssh接続してみます。
また新しい作業ディレクトリを作成して、init後、Vagrantfileに1行追加します。

```
$ mk /your/directory/vm3
& cd /your/directory/vm3
$ vagrant init centos/7
$ vi Vagrantfile
```

Vagrantfileに１行追加
```
config.vm.network "private_network", ip: "172.100.1.2"
```

VMに対してホストOS以外のIPにsshでログインできるようになりました。
```
$ vagrant up
$ ssh -i /your/directory/vm3/.vagrant/machines/default/virtualbox/private_key vagrant@172.100.1.2
[vagrant@xxx ~]$ 
```
