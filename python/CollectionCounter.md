# Collection Counter in Python

> A Counter is a dict subclass for counting hashable objects. It is a collection where elements are stored as dictionary keys and their counts are stored as dictionary values. Counts are allowed to be any integer value including zero or negative counts. The Counter class is similar to bags or multisets in other languages.

<br>

```python
counter = Counter([1, 2, 3, 4, 2])
counter.most_common(1)                  # (2, 2)
counter[1]                              # 1
del counter[1]
```

<br>

```python 
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
# Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```
