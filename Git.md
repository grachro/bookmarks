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
