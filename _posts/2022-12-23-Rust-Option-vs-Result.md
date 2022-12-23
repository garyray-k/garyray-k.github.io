---
published: false
---
From the [Result module docs](https://doc.rust-lang.org/std/result/index.html).

> Functions return Result whenever errors are expected and recoverable. In the std crate, Result is most prominently used for I/O.

Compared to [Option](https://doc.rust-lang.org/std/option/index.html) (much more here but I tried ot grab the TLDR line).

> Type 'Option' represents an optional value

Coming from other languages, I akin `Option` to the `null` of Rust, but much better because Rust's compiler "forces" you to explicitly handle a case where there is no value (`None`) AND the happy path where there is a value `Some(T)`. I put "forces" because you can easily just `.unwrap()` the `Option` and the code 'Just Works'. This can be when you're rapidly prototyping and don't want to handle the `None` at the moment. Or your code has some checks where you're certain there's a value there (maybe you used `if option.is_some() {...` and you're in the postive case.

For `Result`, I would akin returning a result to throwing an exception, except it's the return type of a function. Again, the compiler will "force" you to handle both scenarios: `Ok(T)` and `Err(E)`. The `Result`'s module doc linked above actually has the following example, that I think is pretty neat combining the two (comments mine): 

```rs
#[derive(Debug)]
enum Version { Version1, Version2 }

fn parse_version(header: &[u8]) -> Result<Version, &'static str> {
    match header.get(0) { // this match is to enumerate all arms of the scenario
        None => Err("invalid header length"), // we received a "null" so "throw" one type of error
        Some(&1) => Ok(Version::Version1), 
        Some(&2) => Ok(Version::Version2),
        Some(_) => Err("invalid version"), // The underscore is the default case. Here the value wasn't as expected, so again "throw" an error
    }
}

let version = parse_version(&[1, 2, 3, 4]);
match version { 
    Ok(v) => println!("working with version: {v:?}"),
    Err(e) => println!("error parsing header: {e:?}"),
}
```

In the above the `.get()` method returns an `Option` which we then pattern match and return a `Result`. The `parse_version` method might fail so it returns a `Result`, whereas `.get(0)` might be called on an empty array or have an invalid value returned. 

(thnx to [Hunter Beast](https://twitter.com/cryptoquick/) for some pondering on this last paragraph) 

> In short, Result is a representation of fallibility, whether something can fail, and Option is a representation of nullibility, whether something can be null. A Result is for when you call a method and if it fails, Result::Error is returned, and Result::Ok is for when it succeeds. Option is for when you know a value might not be present, and to handle that in a similar way, except this time, using Option::Some and Option::None. 


Hope this is as clear as mud.
