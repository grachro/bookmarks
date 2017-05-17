## プロジェクトディレクトリを作成

```
$ mkdir centos7
$ cd centos7
```

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




```
$ vagrant ssh-config
```



## VirtualBoxのVMを停止・削除

```
$ vagrant destroy
```
