### Installing Gems (Packages)
- use bundler - [bundler.io](bundler.io)

### Module
- module vs. class?
  - you can instatiate a class, but you can't instatiate a module
- use a module when you have a state, use a class when you don't

### Methods + Params
def upcase_name(first_name='', last_name)
def upcase_name(first_name = nil, last_name = '') # has default/optional params
def upcase_name(first_name:, last_name:) # named params - generally want to use this for public methods!!! so that external callers can be more successful :-)
def upcase_name(params = {}) # lets ruby know that `params` will be a hash 

### Bang Methods
- `d a n g e r`

### Blocks
```
class Test
  def with_logging(name)
    "Starting #{name}"
    yield # this is the block! the `test` method will basically get plugged in here
    "Finished #{name}"
  end
  
  def test
    with_logging("test") do
      puts "We are here"
    end
  end
end
```

- Generally, use attribute readers instead of instance variables in classes to make your life easier!!!
```
def initialize(woo)
  @woo = woo
end

def foo
  woo / 2
end

def method
  foo
end
```

### Namespacing
- prepend `::` in front to tell Rails to use the `root` namespace

### Inheritance and Mix-Ins
```
class A
  def foo
    puts "foo"
  end
end

class B < A # B inherits from A
  def foo
    puts "blah"
  end
end

B.new.foo # will print "blah"
```

### Private Methods
```
class A
  def foo
    puts "foo"
  end
  
  private
  
  def boo
    puts "boo"
  end
end

A.new.send(:boo) # send takes a symbol; this is how you can call private methods - ONLY USE THIS FOR DEBUGGING
```
  
