### 変数表示

```
[(${変数})]
```

### 別のテンプレートファイルをinsert

Thymeleaf 3.0 Tutorial
http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html

#### insertするファイル名を動的に変える

```
[# th:insert='sub/Foo__${varNumber}__.html'/]
```

### 日付フォーマット
```
[(${#dates.format(new java.util.Date(),'M/d')})]
```

### 数値フォーマット
```
[(${#numbers.formatInteger(1234,3,'COMMA')})]
```

http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#numbers


### if

```
[# th:if="${param}==false"]
param is false
[/]
```
http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#escaped-element-attributes

### switch

```
[# th:switch="${param}"]
  [# th:case="1"]foo[/]
  [# th:case="2"]bar[/]
  [# th:case="3"]baz[/]
[/]
```
### loop

```
[# th:each="item : ${itemList}"]
  this is loop block [(${item.name})]
[/]
```

### コメント
```
/*[- This code will be removed at Thymeleaf parsing time! -]*/
```
- 3.3 Textual prototype-only comment blocks: adding code http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#textual-prototype-only-comment-blocks-adding-code
- https://github.com/thymeleaf/thymeleaf/issues/395

