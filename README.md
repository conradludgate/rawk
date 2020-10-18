# rawk
Awk like syntax macro for handling streams in rust

## What

```rs
let mut x = 0
let parser = rawk!{
	$1 == "0" { format!("found {}", $0) }
	$1 == "1" { #x = #x + 1; "incrementing"}
}
let mut in = "0 foo bar
	1 baz qux
	1
	1
".as_bytes();
let mut out = parser.parse(&mut in);

let mut buf = String::new();
out.read_to_string(&mut buf)?;

assert_eq!(buf, "found 0 foo bar
	incrementing
	incrementing
	incrementing
");
assert_eq!(x, 3);
```

