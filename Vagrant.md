
## インストール
- VirtualBox https://www.virtualbox.org/
- Vagrant https://www.vagrantup.com/

```
$ vagrant --version
Vagrant 1.9.4
```

## Vagrantプロジェクトの初期化からVM起動まで

```
$ mkdir -p /your/directory/vm1
$ cd /your/directory/vm1

#初期化。Vagrantfileが作成されます。
$ vagrant init centos/7

#VirtualBoxにVMを起動
$ vagrant up

#ログイン
$ vagrant ssh

#VirtualBoxのVMを停止・削除
$ vagrant destroy
```

## ssh login
### Vagrantで立ち上げたVMにディフォルト設定でssh(not 'vagrant ssh')でログイン

my memo http://qiita.com/grachro/items/4d34a43a9a57946f3693

```
# SSH接続情報を確認
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


#ディフォルトでは、ホストOSのport 2222に、VMのport 22がフォワードされています。
#このため、localhostのport 2222に対してsshでログインできます。
#選んだOSによってはUserがvagrant以外になっているかもしれません。
$ ssh -i /your/directory/vm1/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@127.0.0.1
とか
$ ssh -i /your/directory/vm1/.vagrant/machines/default/virtualbox/private_key -p 2222 vagrant@localhost

[vagrant@localhost ~]$ 
# su -でrootになる場合、パスワードはvagrantです。
```


### VMに接続するポートを変えてsshログイン

Vagrantfileに１行追加
```
config.vm.network "forwarded_port", guest: 22, host: 2223, id: "ssh"
```

sshログイン
```
$ vagrant up
$ ssh -i /your/directory/vm2/.vagrant/machines/default/virtualbox/private_key -p 2223 vagrant@localhost
[vagrant@xxx ~]$ 
```

### VMのipを変えてsshログイン

Vagrantfileに１行追加
```
config.vm.network "private_network", ip: "172.100.1.2"
```

sshログイン
```
$ vagrant up
$ ssh -i /your/directory/vm3/.vagrant/machines/default/virtualbox/private_key vagrant@172.100.1.2
[vagrant@xxx ~]$ 
```


## 複数VM起動

https://www.vagrantup.com/docs/multi-machine/index.html

```
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "web" do |web|
    web.vm.box = "apache"
    db.vm.network :private_network, ip: "xxx.xxx.xxx.xxx"
  end

  config.vm.define "db" do |db|
    db.vm.box = "mysql"
    db.vm.network :private_network, ip: "xxx.xxx.xxx.xxx"
  end
end
```
