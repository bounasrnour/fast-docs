# Rust

## Data types and variables

variables in rust are immutable to make them mutable add mut

```rust
let x = 5;
let mut y = 5;
//i8 u8 i16 u16 i32 u32 i64 u64 signed unisigned integer
//isize usize depends on the computer size 32 bits or 64 bits
//f32 f64 floats f64 double precision
//we can also specify data type directly
let c:char = 'c';
let b:bool = true;
let i:int = 10;
let t: (i32, f64, char) = (42, 6.12, 'j'); //tuple
let z, y, z = t //destructuring 
let (_, _ , x) = t; // ignore using _
//arrays
let a = [1,2,3,4,5,6]
a1 = a[0];
```

## Tuples

```rust
let t = (1,2,3);
println!('{} {} {}', t.0, t.1, t.2);
println!('{:?}', t); //debug flag :? # to prettify :#?
```

## Arrays

```rust
let a : [i32; 5] //size 5 type i32 = [3,1,2,3,4];
a,ken() //lenght
use std::mem; //for memory functions
mem::size_of_val(&a);
//slicing
let b = &a[2..5]; //2 to 4
```

## Strings

using "text" in rust if a compound character while creating a string using a string method you get an actual string 

```rust
let s = "ansd".to_string();
let ss = String::from('asd');
//those above are strings

//concatenate strings with 
let w = String::from('world')
let slice = h + &w; //reference to w
```

## Ownership

memory allocation, stack and heap , ownership is a little les than a garbage collection, each variable can have only 1 owner example let x = 1;
x is the owner of 1

```rust
let s = String::from('asd');
let y = s;
println!("{}", s); //will throw an error because s is now referecing to nothing
//to prevent that we use a reference to s
let y = &s;

```



## Struct

```rust
struct Object{
  width:u32,
  height: u32,
}

fn area(obj: Object) -> u32{
  obj.width * obj.height
}
//we can ommit return , rust will automatically return
fn main(){
  let o = Object{
    width:14,
    height35,
 
  }
}
//a better way to bind functions to struct using the implement 
imp Object{
  fn area(&self) -> u32{
    self.width * self.height
  }
  //to create a new object
  fn new(width: u32, height: u32) -> Object{
    Object{
      width:width, //we can ommit width height bcz same name
      height:height,
    }
  }
}
//usage
o.area();
let obj = Object::new(32,14);
```

## loop

loop{
//infinite loop
if c == 10{
break;

}}

we can label loops in rust 'a: loop{} and use break 'a

while

```rust
let mut n = 10;
while(n < 0){
  n = n-1;
}
```

for

```rust
let a = vec![10,20,10];
for i in a{
  
}
for i in 1..101{
  
}
```

match

```rust
match x{
  1 = > print,,,
  _ => default case
  3 | 5 | 10 => or
  12...14 => range
  
}
```

## Enums

```rust
enum Direction{
  Up(u32, u32),
  Dow(u32, u32),
  Left(u32, u32),
  Right(u32, u32),
}
fn main(){
  let u = Direction::Up(Point {x: 0, y: 1});
}
```

## ref

```rust
let u = 10;
let ref z = u; //same as let k = &u;
```

## option

```rust
enum Option<T>{
  Some(T),
  None,
}
```

## Vectors

resizable arrays(grow and shrink)

```rust
let x = vec![1,2,4];
let mut v = Vec::new();
v.push(5);
v.push(10);
v.len()
v.capacity();
v.pop();
```

## HashMap

```rust
use std::collections::HashMap;
//dictionaries in python
let mut hm = HashMap::new();
hm.insert(String::from("hh"),12);
//should be same type

for(k, v) in &hm{
  println!('{} {}', km v);
}

match hm.get(&String::from("hh")){
  Some(&n) => println!("{}", n);
  _ => println!("no match");
}

hm.remove(&String::from("key"));
```

