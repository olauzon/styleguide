Ruby Style Guide
================

Please note: This is a work in progress
---------------------------------------

I'm making changes to the guidelines, according to my personal
preferences, and adding code examples to support each point.

Eventually, I'd also like to include JavaScript and other languages.
See (Felix's Node.js Style Guide)[http://nodeguide.com/style.html] for a
Node.js Style Guide template.

Formatting
----------

* Use ASCII (or UTF-8, if you have to).

* Use 2 space indent, no tabs.

* Use Unix-style line endings.

* Use spaces around operators, after commas, colons and semicolons,
  around { and before }.

* No spaces after (, [ and before ], ).

* Use two spaces before statement modifiers (postfix
  if/unless/while/until/rescue).

* Indent when as deep as case.

* Use an empty line before the return value of a method (unless it
  only has one line), and an empty line between defs.

* Use RDoc and its conventions for API documentation.  Don't put an
  empty line between the comment block and the def.

* Use empty lines to break up a long method into logical paragraphs.

* Keep lines fewer than 80 characters.

### Kill all whitespace all the time

#### Good

```ruby
class Account

  def credit
  end

  def debit
  end

end
```

#### Bad

With whitespace represented with a `#`

```ruby
class Account

  def credit
  end
##
  def debit
  end

end
```

#### Even worse

With whitespace represented with a `#`

```ruby
class Account###
##
  def credit######
  end
##
  def debit#
  end#
####
end###
######
```

Syntax
------


### Use `def` with parentheses when there are arguments

```ruby
# Good
def add(user)
  # 'user' is clearly an argument
end
```

```ruby
# Bad
def add user
  # It's not clear what 'user' is
end
```

* Never use for, unless you exactly know why.

* Never use then.

* Use when x; ... for one-line cases.

* Use &&/|| for boolean expressions, and/or for control flow.  (Rule
  of thumb: If you have to use outer parentheses, you are using the
  wrong operators.)

* Avoid multiline ?:, use if.

* Suppress superfluous parentheses when calling methods, but keep them
  when calling "functions", i.e. when you use the return value in the
  same line.

    x = Math.sin(y)
    array.delete e

### Prefer `{...}` over `do...end`


#### Good

```ruby
accounts.each { |account| account.charge! }
```

#### Not as good

```ruby
accounts.each do |account|
  account.charge!
end
```

* Multiline {...} is fine: having
  different statement endings (} for blocks, end for if/while/...)
  makes it easier to see what ends where.  But use do...end for
  "control flow" and "method definitions" (e.g. in Rakefiles and
  certain DSLs.)

### Avoid `do...end` when chaining


#### Good

```ruby
1.upto(10).select { |n| n % 2 == 1 }.map { |n| n * 100 }
```

#### Good

It's encouraged to use parentheses when it makes it clearer

```ruby
1.upto(10).select { |n| (n % 2) == 1 }.map { |n| n * 100 }
```

#### Acceptable

It's acceptable to omit the space after `{` and before `}`

```ruby
1.upto(10).select {|n| n % 2 == 1}.map {|n| n * 100}
```

#### Not as acceptable

It's not as acceptable to omit the space before `{`

```ruby
1.upto(10).select{|n| n % 2 == 1}.map{|n| n * 100}
```

#### Bad

```ruby
1.upto(10).select do |n| n % 2 == 1 end.map do |n| n * 100 end
```

#### Worse

Mixing `{...}` and `do...end` when chaining is even worse

```ruby
1.upto(10).select do |n| n % 2 == 1 end.map { |n| n * 100 }
```

### Avoid `return` where not required


#### Good

```ruby
def tax
  price * tax_rate
end
```

#### Bad

```ruby
def tax
  return price * tax_rate
end
```

#### Worse

```ruby
def tax
  amount = price * tax_rate
  return amount
end
```


* Avoid line continuation (\) where not required.

### Using the return value of `=` is acceptable

#### Good

It is preferable to enclose the expression in parentheses

```ruby
if (amount = account.outstanding_amount)
  # Do something with 'amount'
end
```

It is acceptable to omit parentheses when there is a single expression

```ruby
if amount = account.outstanding_amount
  # Do something with 'amount'
end
```

#### Not as good

When there are multiple conditions, it using the return value of `=` doesn't
work quite as well

```ruby
if (amount = account.outstanding_amount) && account.active?
  # Do something with 'amount'
end
```

#### Better

It's better to break it down into multiple statments

```ruby
amount = account.outstanding_amount
if amount && account.active?
  # Do something with 'amount'
end
```

### Use `||=` freely

#### Good

```ruby
def amount
  # `calculate_amount` is an expensive operation
  @amount ||= calculate_amount
end
```

#### Bad

```ruby
def amount
  # `calculate_amount` is an expensive operation
  calculate_amount
end
```

* Use non-OO regexps (they won't make the code better).  Freely use
  =~, $0-9, $~, $` and $' when needed.


Naming
------

* Use snake_case for methods.

* Use CamelCase for classes and modules.  (Keep acronyms like HTTP,
  RFC, XML uppercase.)

* Use SCREAMING_SNAKE_CASE for other constants.

* The length of an identifier determines its scope.  Use one-letter
  variables for short block/method parameters, according to this
  scheme:

  * a,b,c: any object
  * d: directory names
  * e: elements of an Enumerable
  * ex: rescued exceptions
  * f: files and file names
  * i,j: indexes
  * k: the key part of a hash entry
  * m: methods
  * o: any object
  * r: return values of short methods
  * s: strings
  * v: any value
  * v: the value part of a hash entry
  * x,y,z: numbers

    And in general, the first letter of the class name if all objects
    are of that type.

* Use _ or names prefixed with _ for unused variables.

* When using inject with short blocks, name the arguments |a, e|
  (mnemonic: accumulator, element)

* When defining binary operators, name the argument "other".

* Prefer map over collect, find over detect, find_all over select,
  size over length.


Comments
--------

* Comments longer than a word are capitalized and use punctuation.
  Use two spaces after periods.

* Avoid superfluous comments.


The rest
--------

* Write ruby -w safe code.

* Avoid hashes-as-optional-parameters.  Does the method do too much?

* Avoid long methods.

* Avoid long parameter lists.

* Use def self.method to define singleton methods.

* Add "global" methods to Kernel (if you have to) and make them private.

* Avoid alias when alias_method will do.

* Use OptionParser for parsing complex command line options and
  ruby -s for trivial command line options.

* Write for 1.8, but avoid doing things you know that will break in 1.9.

* Avoid needless metaprogramming.


General
-------

* Code in a functional way, avoid mutation when it makes sense.

* Do not mutate arguments unless that is the purpose of the method.

* Do not mess around in core classes when writing libraries.

* Do not program defensively.
  (See http://www.erlang.se/doc/programming_rules.shtml#HDR11.)

* Keep the code simple.

* Don't overdesign.

* Don't underdesign.

* Avoid bugs.

* Read other style guides and apply the parts that don't dissent with
  this list.

* Be consistent.

* Use common sense.


Credits
-------

Based largely on [Christian Neukirchen](http://chneukirchen.org/blog/)'s [Ruby Style Guide](https://github.com/chneukirchen/styleguide).

### Contributors

* [olauzon](https://github.com/olauzon/styleguide)
* [theIV](https://github.com/theIV/styleguide)
