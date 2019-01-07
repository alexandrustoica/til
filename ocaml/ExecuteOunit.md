#### Execute Ocaml Unit Test with ocamlbuild

**Problem**: Execute a given ocaml unit test file `tests/XTest.ml` using `ocamlbuild`

```ocaml
open OUnit2

let tests = "test suite for sum" >::: [
"empty"  >:: (fun _ -> assert_equal 0 0);
"one"    >:: (fun _ -> assert_equal 1 1);
"onetwo" >:: (fun _ -> assert_equal 3 2);
]

let _ = run_test_tt_main tests
```

**Solution**:
```bash
$ ocamlbuild -r -package oUnit tests/XTest.byte
$ ./XTest.byte
$ ./rm XTest.byte # clean up 
```
