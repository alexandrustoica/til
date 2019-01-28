
### Filters & Selectors in AppleScript
AppleScript uses the keywords `whose` and `where` to filter the content of a list of objects, based on a given predicate/property. The keywords `first` and `every` are selectors.

```applescript 
set completedTasks to (every flattened task whose completed is true)
```


```applescript 
set firstCompletedTask to (first flattened task whose completed is true)
```

```applescript 
set <result_list> to (every <list> whose <predicate>)
```

```applescript 
set <result_list> to (every <list> where (<predicate>))
```
