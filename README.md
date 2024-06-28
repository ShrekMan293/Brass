# Zephyr
A statically typed language that I hope can be a long term project that is updated constantly

## Name Origin
**I named it Zephyr with two reasons in mind:**
1. A zephyr is a light wind, I don't want this to be a big heavy language. I want it to be lightweight
2. Also a tribute to my hometown: New Orleans, New Orleans used to have a baseball team named the Zephyrs, hence Zephyr

## Syntax
### Types
Floating point values are approximate
| Type Name | Min Value to Max Value | Example Usage |
| :---------|:----------------------:|:--------------|
| i8        | -128 to 127            | ```iden : i8 = 12```|
| u8        | 0 to 255               | ```iden : u8 = 20```|
| i16       | -32768 to 32767        | ```iden : i16 = 3200```|
| u16       | 0 to 65536             | ```iden : u16 = 53029```|
| i32       | -2147483648 to 2147483647 | ```iden : i32 = x```|
| u32       | 0 to 4294967295        | ```iden : u32 = 3029```|
| f32       | -3.40282347 × 10^38 to 3.40282347 × 10^38 | ```iden : f32 = 31.283```|
| f64       | -1.7976931348623157 × 10^308 to 1.7976931348623157 × 10^308 | ```iden : f64 = 382.2930```|
| i64       | -9223372036854775808 to 9223372036854775807| ```iden : i64 = 20```|
| u64       | 0 to 18446744073709551615 | ```iden : u64 = 2994```|
| let      | '\0' to '\255' | ```iden : let = 'J'```|
| string | Only limit is memory | ```iden : string = "Hello World!"```|
| type | Depends on the declaration | More data below|

### Operators
Or is not a real operator, it's '|', but markdown uses the pipe
Compound operators nnot included
| Characters |     Usage     |
|:----------:|:-------------:|
| + | 3 + 4 |
| - | 5 - 2 |
| * | 3 * 5 |
| / | 12 / 4 |
| = | i = 3 |
| & | 3 & 2 |
| or | 4 or 2 |
| ~ (not) | 3 ~ 6 |
| ^ (xor) | 4 ^ 2|

### Keywords
| Name     |         Usage         |
| :--------|:---------------------:|
|

### Functions
Declare a function with the syntax ```func iden(args) : type```

**If a function has no type, void is assumed**

```
func hello() : i32 {
    lock msg : string = "Hello World!\n";
    print msg;
}
```

### Type Declarations
```
type Animal (
    string name
    u8 age
);
## Any type can have an impl

impl Animal {
    func ageAnimal() {
        this.age++;
    }
    func (string name, u8 age) {    ## Declares a constructor
        this.name = name;
        this.age = age;
    }
};

lock bear : Animal = Animal("Bear", 0);
```
