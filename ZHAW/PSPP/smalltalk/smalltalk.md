
### Oddities



<ul style="color:red; font-size: xx-large;">
	<li>Arrays start at 1</li>
	<li>Mathematical operator precedence does not apply</li>
</ul>


#### General
- **PURE** OOP
- **EVERYTHING** is an [[#Objects (& Classes)]]
- **[[#Messages]]** are the only way for communication between objects 
	- [[#Message Cascade]] expression `;`, messages get sent in sequence
- statements terminated with `.` dot
	- **Last dot is optional**
 ```smalltalk 
x := Array new: 2. 
x at: 1 put: 5 ;
	at: 2 put 10 .
```
- blocks in `[ ...... ]`
- single inheritance
- state is private (protected for sub-classes)
- all Methods are public
- comments in `"` double quoutes
- `3@4` constructs a point x=3, y=4 (careful with -)
#### Conditions 
http://rigaux.org/language-study/syntax-across-languages-per-language/Smalltalk.html
- `== / ~~` compares whether both are the same **Object**
- `= / ~=` compares whether both are **Equal**
	- defaults to `==` if not overriden
- `True` and `False` are also classes, `true` & `false` are unique instances of these
	- used together with `ifTrue/False:` messages
 - regular logical operators (`&`) are eager (also executes if left = false)
	 - `:and` behaves lazily like expected from `&&` in other languages
```smalltalk
Transcript show: ( (3 > 2) ifTrue: ['heloo'] ifFalse: ['lelo'] ). 
```
#### Blocks
like lambdas
- **NOT EXECUTED** unless `value` is called

```smalltalk
[Transcript show: 'elo'] value. "elo"
[:x :y| x + y] value:3 value: 5. "8"
```

```rust
(|| print!("elo"))(); // elo
(|x, y| x + y)(3, 5); // 8
```
#### Loops

**Inclusive** for loop
```smalltalk
1 to: 100 by: 3 do:
	[:i | Transcript show: i asString; cr ].
"while loop"
"condition MUST be in bracket, unlike if (since its a block getting called)"
[i < 100] whileTrue: [
	sum := sum + i.
	i := i + 1;
]
"iterators"
"for-each"
#(11 38 3 -2 10) do: [:ele | Transcript show: each asString; cr]
					separatedyBy: [Transcript show: '.'].
"map"
#(11 38 3 -2 10) collect: [:ele | ele odd]. "#(true false true false false)"
"filter"
#(11 38 3 -2 10) select: [:ele | ele odd]. "#(11 3)"
#(11 38 3 -2 10) reject: [:ele | ele odd]. "#(38 -2 10)"
```


#### Numbers
- has builtin fractions like $\large 1/3 + 4/5 = 17 / 15$
- numerical types automatically convert
#### Text
- characters with '\$', `$A` = the character 'A'
- strings with `'` single quotes
- concatenation with the comma operator` 'Hello','World'` 
#### Symbols 
- Symbols are globally unique Strings(all share the same instance)
- read only (Strings are mutable like everything else)
- used as method selectors and unique keys in dictionaries
```smalltalk
#'A string preceded by a hash sign is a Symbol'
#orAnyIdentifierPrefixedWithAHashSign
#orAnIdentifierEndingWithAColon:
#or:several:identifiers:each:ending:with:a:colon:
```
#### Arrays
- **START AT 1**
- literal arrays `#(1 2 3)`
- dynamic arrays: `x := Array new: 4.`
	- `x at 1 put 5.`



#### Variables
- declared with `| x y |`
- assign with `x := 1`
#### Pseudo Variables
- nil -> UndefinedObject
- true/false -> [[#Conditions]]
- self -> Reference to this object, method lookup starts in object's class
- **super** -> Reference **to THIS object**, method lookup starts at **superclass**


## Messages
(sometimes Selectors)

### Execution Order
[[#Unary Messages]] -> [[#Binary Messages]] -> [[#Keyword Messages]]

<ul style="color:red">
	<li>Mathematical operator precedence does not apply -> left to right</li>
</ul>

**Equal precedence -> left-to-right**

```smalltalk
2 raisedTo: 3 + 2. "32" "!!!!!!"
(2 raisedTo: 3) + 2. "10"
-3 abs negated reciprocal. "(-1/3)"
-2 + 2 * 10. "0 !!!!!!!!!!!!"
```

Sent to objects
#### Unary Messages

```smalltalk
1 class. "SmallInteger"
false not. "true"
```
#### Binary Messages

```smalltalk
3 * 2. "6"
Date doay + 3 weeks. "22 January 2024"
false | false. "false"
'ab','cd'. "'abcd'"
```
#### Keyword Messages
Messages with arguments
```smalltalk
anObject aKey: anotherObject [ anotherKey: anotherObject 2 ]
4 between: 0 and: 10. "true"
Point new setX:4 setY:5. "(4@5)"
1 max: 3. "3"
```


### Message Cascade

`;` Operator, pass message to same receiver

```smalltalk
Transcript
	open;
	show: 'hello';
	show: 'lelo';
	cr.
```





## Objects (& Classes)

- Instantiated with `SimpleButton new.`
	- anonymous object can be used `SimpleButton new openCenteredInWorld.`
- `SimpleButton allInstances` returns an array with all instances of this class

#### Predefined Methods (Messages)

- `class` -> return receiver class
- `isKindOf: aClass` -> is aClass superclass of receiver
- `respondsTo: aSymbol` -> whether the class (or superclass) understands the message
- `==/~~`, `=/~=` -> [[#Conditions]]
- `isNil`
- `copy`
- `shallowCopy`
- `deepCopy`

### Define new Classes

```smalltalk
Object subclass: #NameOfNewClass
	instanceVariableNames: '' "analogous to protected"
	classVariableNames: ''
	poolDictionaries: ''
	category: 'Lelo'

Number subclass: #Complex
	instanceVariableNames: 'real img'
	classVariableNames: ''
	poolDictionaries: ''
	category: 'ComplexNumbers'
```

### Define Methods (Messages)

```smalltalk
">> indicates that real is part of the class Complex"
"getter"
Complex >> real
	^real "^ is return"
"setter"
Complex >> real: val
	real := val

"local variables with |var|"
SomeClass >> someMethod: val
	|var|
	mystery = val + var
```

