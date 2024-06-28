## Syntax
### Types
Floating point values are approximate
| Type Name | Min Value to Max Value | Example Usage |
| :---------|:----------------------:|:--------------|
| bool      | 0 (false) to 1 (true)  | ```iden : bool = false```|
| i8        | -128 to 127            | ```iden : i8 = 12```|
| u8        | 0 to 255               | ```iden : u8 = 20```|
| i16       | -32768 to 32767        | ```iden : i16 = 3200```|
| u16       | 0 to 65536             | ```iden : u16 = 53029```|
| i32       | -2147483648 to 2147483647 | ```iden : i32 = x```|
| u32       | 0 to 4294967295        | ```iden : u32 = 3029```|
| f32       | -3.40282347 × 10^38 to 3.40282347 × 10^38 | ```iden : f32 = 3.14159265358979323```|
| f64       | -1.7976931348623157 × 10^308 to 1.7976931348623157 × 10^308 | ```iden : f64 = 382.2930```|
| i64       | -9223372036854775808 to 9223372036854775807| ```iden : i64 = 20```|
| u64       | 0 to 18446744073709551615 | ```iden : u64 = 2994```|
| let       | '\0' to '\255'          | ```iden : let = 'J'```|
| list      | Only limit is memory    | ```iden : list = list::create()```|
| string    | Only limit is memory    | ```iden : string = "Hello World!"```|
| type      | Depends on the declaration   | More data below |
| void      | No value                | ```func f() : void```|

### Operators
Binary Or is not a real operator, it's '|', but markdown uses the pipe
Logical or is '||'
Compound operators not included in this file but they do exist
++, --, +=, *=, -=, /=, %=, |=, etc
| Characters |     Usage     |
|:----------:|:-------------:|
| + | 3 + 4 |
| - | 5 - 2 |
| * | 3 * 5 |
| / | 12 / 4 |
| % | 15 % 6|
| = | i = 3 |
| & (binary) | 3 & 2 |
| or (binary) | 4 or 2 |
| ~ (not (binary)) | 3 ~ 6 |
| ^ (xor) | 4 ^ 2|
| == | return i == 2|
| and (logical) | if b && i == 2 |
| or (logical) | if b or i == 2 |
| ! (not(logical))| b : bool = !true |
| => | 1 => print 1 |
| * | c_function(*i) |
#### Separators
| Characters | Usage |
|:----------:|:-----:|
| :: | ```comp::Animal```|
| ; | ```string s;``` |
| , | ```func test(string s, i16 i)```|
| : | ```iden : list``` |
| ( | ```func bob ()``` |
| ) | ```func bob ()``` |
| { | ```() : i32 {``` |
| } | ```return 12; }```|
#### Literals
| Characters | Usage |
|:----------:|:-----:|
| _ | ```_ => print "default"```|
| $ | ```s : string = $"hi {time}"```|
| " | ```s : string = "hi"```|
| ' | ```c : char = 'c'```|
|0-9| ```i : i8 = 255``` |
| 0x0-F | ```i : i8 = 0xFF``` |
| 0b0-1| ```i : i8 = 0b11111111```|
| identifiers | a-zA-z_0-9 |

### Keywords
'or' and 'and' are alternatives to || and &&
| Name     |         Usage         |
| :--------|:---------------------:|
| and | ```if b and i == 2```|
| bool | ```iden : bool = true``` |
| break | ```1 => print 1; break;``` |
| cast<>| ```iden : i64 = cast<i64>(x)```|
| catch | ```catch (Exception)```|
| codespace | ```codespace comp;```|
| elif | ```elif i == 5``` |
| else | ```else {```|
| entry | ```entry {```|
| enum | ```type test : enum (``` |
| extern | ```extern func ctime()```|
| for | ```for i = 0; i < 4; i++```|
| foreach | ```foreach i8 in iden``` |
| func | ```func test() : i32``` |
| if | ```if i == 2``` |
| ignore| ```ignore 0x90210```|
| impl | Example below |
| import | ```import code.zph```|
| in | ```foreach i16 in iden```|
| lock | ```lock i : i8 = 12```|
| macro| ```macro assign (code)```|
| new | ```new cast<i64>()```|
| null | ```i = null```|
| or | ```if b or i == 2```|
| packed | Example below |
| precomp | ```precomp func test() : u8```|
| print | ```print i```|
| spread | Example below |
| switch | Example below |
| try | ```try {```|
| type | Example below |
| unlock | ```unlock iden;```|
| unsafe | ```unsafe {```|
| using | ```using comp```|
| var    | ```v : var = Animal()```|
| while | ```while i == 5```|

### Type Declarations
```
type Animal (
    string name
    u8 age
);
## Any type can have an impl

impl Animal {
    func ageAnimal() {
        this::age++;
    }
    func (string name, u8 age) {    ## Declares a constructor
        this::name = name;
        this::age = age;
    }
};

trait Color of Animal { # of is the keyword that defines the parent of the trait
    # A trait is like a child class, a parent can have as many traits as it wants
    u8 alpha
    u8 red
    u8 green
    u8 blue

    func getColor() {
        print red;
        print green;
        print blue;
    }
};

lock bear : Animal = Animal("Bear", 0); # Makes bear immutable

func testTrait() {
    bear::Color::getColor();
}
```
#### Type Declaration Modifiers, confusing name but not to be confused with Variable Modifiers
Specifically ```packed``` and ```spread```
##### Packed
Packed has 0 padding and puts everything as close as possible
##### Spread
Spread has two usages, spread it out as much as the compiler feels is necessary, probably 2 bytes in between each variable and however many at the end
**OR**
```spread(size)``` Spreads it evenly to the specified size

#### Functions
Declare a function with the syntax ```func iden(args) : type```

**If a function has no type, void is assumed**

```
func hello() : i32 {
    lock msg : string = "Hello World!\n";
    print msg;
}
```
##### Compile Time Functions
Some functions need to be run with max precision                                                                                        
Compile time functions allow them to be converted to binary during compilation to run faster at runtime
- Could slow down compilation

```
precomp func time() {
    print extern time;
}
```
##### Entry Function
The program needs to enter somewhere, if no entry is specified it may not run correctly

```
entry {
    print "Hello World!\n";
}
```
Pretty much like the main() function, and yes you can get arguments

### Ignore and Macro
#### Ignores
```ignore 0x90210```
Would tell the compiler to ignore WARNING 0x90210, errors cannot be ignored

#### Macros
```
macro assign(Agent("Perry", Animal("Platypus, 1), Person("Phineas, 10)))
perry : Agent = assign;
```

### Operator Overloading and Cast Declaring
#### Operator Overloading
```
new +(type iden, type iden) : type
```
#### Cast Declarations
```
new cast<type>(type) {}
```

### Switch Cases
Taken right out of the book from C#, C# has regular C style switch blocks and switch expressions                                                                                         
These switch cases are assignable since they are expressions
```
switch (op) {
    1 => do stuff; break;
    _ => do stuff; break; ## Default
}
```

### Comments
```## Single Line Comment```
```
###
# Multi
# Line
# Comment
###
```

### Unsafe Code
#### External Functions
If you want to use code that isn't supported in Zephyr, I bring you external functions

Using the ```extern``` keyword, you can access linked C/C++ functions

```
time : u64 = extern func ctime();
```

***BUT***

Back to unsafe code, all extern functions must be in an unsafe block                                                                    
Unsafe blocks are also compiled to binary, so they pretty much have a ```precomp``` before them                                         
But although unsafe = precomp, precomp != unsafe

#### Why is there unsafe code?
The compiler wants to generate the most efficient and safe code possible, but with unsafe code, unexpected things could happen                                                           
The compiler has no control over the possibilities so unsafe just tells the compiler to compile it to binary and leave it alone                                                          
#### When should I use unsafe code?
When calling any external functions, using pointers, or changing variable mutability                                                                                                     
Pretty self explanatory but any program with an unsafe block must be marked unsafe

**Example**
```
lock helloMsg : string = "Hello World!";

unsafe {
    time : u64 = extern func ctime();
    unlock helloMsg;
    helloMsg = "Hello World,";
    lock helloMsg;
}

msg : string = helloMsg + $"It has been {time} seconds since midnight";

print msg;
```
