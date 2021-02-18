## Mirroring a repository

```
git clone --bare [old ripository path]

cd [cloned old ripository]
git push --mirror [new ripository path]

cd ..
rm -rf [cloned old ripository]
```

https://help.github.com/articles/duplicating-a-repository/

## git svn clone

```
git svn clone http:/[svnpath] -T trunk
```


## file log
```
# "%x09" is tab
git log --pretty='format:%h%x09%cd%x09%s%x09%d%x09[%an]' --date=iso パス
```
