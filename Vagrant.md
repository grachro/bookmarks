
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


## Vagrantで起動したVMにOracleXEをインストール

```
===========
ホストOS
===========

cd /your/vagrant/directory
ここにOracleのサイトから入手した、oracle-xe-11.2.0-1.0.x86_64.rpm.zipを配置

vagrant init centos/7

vagrant up
vagrant ssh

===========
VM
===========
cd /vagrant

sudo yum update -y

sudo yum install -y vim \
  less \
  unzip \
  bzip2 \
  libaio \
  bc



sudo su -
dd if=/dev/zero of=/swap bs=1024 count=1048576
chmod 0600 /swap
mkswap /swap
swapon /swap
cat /proc/swaps


unzip oracle-xe-11.2.0-1.0.x86_64.rpm.zip 
sudo rpm -ivh Disk1/oracle-xe-11.2.0-1.0.x86_64.rpm

sudo /etc/init.d/oracle-xe configure


#リターン（ディフォルト8080）
#リターン（ディフォルト1521）
#pw
#リターン
#pw
#リターン
#y
#リターン
sudo printf \\n\\n\\npw\\npw\\ny\\n | /etc/init.d/oracle-xe configure
sudo /etc/init.d/oracle-xe start

sudo su - oracle
. /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh


#sqlplus/imp/exp...
```

