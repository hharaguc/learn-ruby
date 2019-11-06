```
* Gem install, ruby gems
* Using ruby to run a file
* method definition, no polymorphism
* Optional, named params
* Braces, curly braces for hash arguments
* Bang methods, boolean methods with ?
* Blocks, yield, block_given?
* returns last value of block
* Exceptions, begin rescue end ensure
* Modules vs classes, initialize/new
* Class method vs instance method, class << self
* Private, send, __send__
* attr_reader, attr_writer, attr_accessor
* Namespace, using :: for root class
* Re-opening classes, monkey patching
* Inheritance vs mixins, include vs extend
* Bundler, gemfile
```

### Linter
- use rubocop

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

## Week 3: ACTIVE RECORD
### What it is
- an ORM: object relational mapping; this means `one model map to one table`
- Active Support :: Active Record as lodash :: javascript
- `bundle exec rake ... # rake is a task runner`

### Some commands
- ** Below, `User` is just an example model`
- CRUD: create | read | update | destroy
- Using `User.find(id: 100)` in the Rails console gives you an `ActiveRecord::Relation`
  - vs. `User.find_by(prefix: "Mr.")` - use regular `.find` when you're searching by ID
- `User.new` vs. `User.create` - `create` will actually save the object, `new` does not
- `.update` vs. `.update_attributes`
- `.update_all`: batch updates
- `User.delete` vs. `User.destroy`
  - `.delete` is not as safe as `destroy`!! because it skips over model validations and hooks
  
- can preload relationships in ActiveRecord to prevent N+1s
  - relationships are lazy loaded
  - Rails lazy loads as much as it can
- can view sql by doing `User.<ActiveRecord command>.to_sql` - V USEFUL




TO DO:
- [ ] Learn about Active Support


## Week 4: Testing!

```
require 'spec_helper'

Rspec.describe ImportJob do
  setup
  before/after/around hooks
  context blocks
    describe blocks
      test
        expectations
        run the code
        assertions
```    
- When you instantiate a new class, use `subject` instead of `let`
```
subject(:import_job) { described_class.new(options: options) }
```

- Around hooks
```
around :each do |example|
  ENV['MY_ENV_VAR'] = true
  example.run
  ENV['MY_ENV_VAR'] = nil
end
```

- Testing instance vs. class methods
```
describe 'ImportJob.create_from_existing' # instance method, use a dot

describe 'ImportJob#parent_options' # class method, use a pound sign
```

### Gotchas
- `let` lazily loads things, will only instantiate the variable when it is referenced in your code
```
let(:another_job) { ImportJob.new }

it 'returns the parents options' do
  parent_options = subject.parent_options
end
```

- Solution: eager load
```
let!(:another_job) { ImportJob.new }
```
