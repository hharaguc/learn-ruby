# learn-ruby
#### Notes on Ruby

- irb: ruby console (interactive ruby)
- Everything in Ruby is an object and inherits from `BasicObject`
- You can get the class of any object by doing `.object`
- You can see the different methods you can call on any object by doing:
  - `.methods`
  - `.public_methods`
- Check if a method can be called on an object by doing `Object.respond_to?(:method)`
- Check if an object is of a certain type by doing `"dane".is_a?(Integer)`
- Don't use triple equals `===`
- Don't use `and` or `or` keywords (they have really low precedence, which can cause weird bugs). Use `&&` and `||`

```
class A
  // this is a class variable - you should never do this because it can cause issues with inheritance and such
  @@variable = "woo" 
  
  // instance variable
  @variable = "woo" 
  
  // local variable
  variable = "woo"
end
```


```
"dane" // this is a string
:dane // this is a symbol!
```
- Why are symbols good?
  - Ruby keeps a table of symbols - symbols can be used in multiple places but will only be instantiated (and create a memory footprint) once
  - `to_sym` adds an object to the symbol table
  
- Ruby `unless` = `if not`
```
return false unless x == 1
```
  
#### Constants
`DANE = 'the best'.freeze // want to put .freeze here to make it immutable`

#### Arrays + Array Literals
- `%w(w, a, d) // is the array literal of ['w', 'a', 'd']; %w means it will be an array of strings`
- `array.first // access the first element in an array`
- `array.last // access the last element in an array`
- `array.map`
```
array = [1, 2, 3]
array.map {|n| n.to_s}
array.map(&:to_s) // shorthand for the above
```

#### Hashes + Accessors
```
hash = { "a": "woo" } // the key is a string
hash["a"]

hash = { a: "woo" }   // the key is a symbol - preferred bc symbols are more performant!
hash[:a]              // THIS SHOULD NOT BE USED bc when a key doesn't exist, it will just return nil
hash.fetch(:a)        // USE THIS! this is better because .fetch will throw an exception when a key doesn't exist
```

```
1..5  // inclusive; => 1, 2, 3, 4, 5

1...5 // exclusive; => 1, 2, 3, 4
```

#### Loops
- Don't use a for-loop! Instead -
```
(1..5).each do
  # do things here
end
```

#### TO DO:
- [ ] Learn Ruby enumerable https://ruby-doc.org/core-2.6.5/Enumerable.html
- [ ] https://ruby.github.io/TryRuby/ 
- Review Ruby style guide
