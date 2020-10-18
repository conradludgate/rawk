# rawk
Awk like syntax macro for handling streams in rust

## What

```rs
let mut x = 0
let parser = rawk!{
	$1 == "0" { format!("found {}", $0) }
	$1 == "1" { #x = #x + 1; "incrementing"}
}
let stdin = io::stdin();
let mut out = parser.parse(stdin);

let mut buf = String::new();
out.read_to_string(&mut buf)?;
```

