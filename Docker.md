## Docker Hub
Docker Hub https://hub.docker.com/

## run

### run CentOS
```
docker run -it --rm centos:7
```


### run Python3
```
docker run -it --rm python:3 /bin/bash
```


### run Elixir
```
docker run -it --rm elixir /bin/bash
```

## image
作成されたローカルのimageを確認
```
docker images
```
## rm

停止したすべてのコンテナを削除(rmコマンド)
```
docker rm -f $(docker ps -aq -f status=exited)
```

## rmi

依存していない不要なimageを全て削除
```
docker rmi $(docker images | awk '/^<none>/ { print $3 }')
```

## volume

### volume一覧
```
docker volume ls
```

### volume削除
```
docker volume rm [your_volume_name]
```


### ホストOS(Mac)上でvolumeの内容を確認

参考: https://forums.docker.com/t/host-path-of-volume/12277/6

```
screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty  

# screen上で
ls -ltrh /var/lib/docker/volumes

#screenから抜ける(control+aの後すぐにkも打つ)
control+a k

```
