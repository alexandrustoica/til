The keyword `as` binds a name to all or a part of a pattern; `as` name binding occurs left-to-right, unlike most languages. `::` appears to have higher precedence than `as`, therefore, `(b :: _ as t)` is equivalent to `((b :: _) as t)`.

``` ocaml
let compress (xs: 'a list): 'a list =
	match xs with
	| h :: (x :: _ as t) -> 
		if h = x 
		then compress t
		else h :: (compress t)
	| any -> any
```
