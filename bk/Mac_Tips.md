マックの使い方ヒント

## tool

### finder plugin

finderからconsolを開く
https://github.com/jbtule/cdto


### MySQL Client
Sequel Pro http://www.sequelpro.com/

### PostgreSQL Client
PSequel http://www.psequel.com/


## command

### ファイル名で検索

```
find [検索対象ディレクトリ] -type f -name [ファイル名のパターン]

とか
find [検索対象ディレクトリ] -type f | grep [ファイル名のパターン]
```

[検索対象ディレクトリ]は、サブディレクトリも対象
 [ファイル名のパターン]は、*.xmlとか
-type f ファイルだけ検索
-type d ディレクトリだけ検索


### ファイル内のキーワドで検索
```
grep -r --include='*.[拡張子]' [検索キーワード]

grep -r --include='*.[拡張子]' [検索キーワード] [検索対象ディレクトリのルート]
```

### ディレクトリの差分を見る
```
diff -qr dirA dirB
```

### 再帰的にディレクトリを作る

```
mkdir -p foo/bar
```


### 指定したパス直下のディレクトリの合計サイズ

```
sudo du -h -x -d 1 /your/directory
```


### ファイルを一括削除

```
mac
find . -type f -print0 | xargs -0 rm

linux
find . -type f -print | xargs rm
```

### バイナリファイルを探す

```
find . -type f -print0 | xargs -0 file | grep -v text 
```
