
## スレッドダンプ

```
jstack <pid> > thread.dump

```


## HEATP DUMP

Eclipse Memory Analyzer http://www.eclipse.org/mat/

## Stream Api

### select count(elm) from list group by elm

```
List<String> list = new ArrayList<>();
Map<String, Long> counted = list.stream()
    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```
