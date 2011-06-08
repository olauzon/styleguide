Ruby Style Guide
================


Please note: This is a work in progress
---------------------------------------

I'm making changes to the guidelines according to my personal preferences, and
adding code examples to support each point.

I'd also like to include JavaScript and other programming languages eventually.
See [Felix's Node.js Style Guide](http://nodeguide.com/style.html) for a Node.js
style guide template.


Goals
-----

This style guide is an attempt to help me identify and understand the subset of
the Ruby programming language I commonly employ. I believe this set of rules and
guidelines yields the most satisfying style to write, and more importantly, read
code in Ruby.

The primary activity of a programmer is not to write code. It is to read code.
This is often code written by the same programmer. Code is most easily read when
its formatting provides cues about its internal structure, and its semantics
reveal knowledge and insight about its domain and purpose. The key
elements of coding style are thus formatting and naming.

Code is useless unless it performs tasks reliably within a reasonable amount of
time. Performance considerations are therefore important factors in developing
and adapting coding style over time.


Disclaimer
----------

I do not write the most beautiful code in the Universe, and following these
guidelines will not necessarily lead to writing beautiful code.


Formatting
----------

### Never use more than _80 characters per line_

This is the single most important rule. If you only follow one rule, please let
it be this rule. Many other rules are derived or altered by this rule.

As an example, suppose you have a long list of options to pass into an
ActiveRecord object

```ruby
Person.create(:first_name => 'Adam', :last_name => 'Smith', :occupation => 'Philosopher', :date_of_birth => '1723-06-23', :karma => 17900717, :email => 'adam.smith@example.com')
```

Without looking at the example again, how many options were there?

Now consider the same example with this formatting

```ruby
Person.create(:first_name     => 'Adam',
              :last_name      => 'Smith',
              :occupation     => 'Philosopher',
              :date_of_birth  => '1723-06-23',
              :karma          => 17900717,
              :email          => 'adam.smith@example.com')
```

The latter example makes it easier to grasp its underlying structure. It is
composed one option per line, and the eye and mind is good at estimating the
number of lines it perceives. (citation needed)

Had there only been two options, we could have written

```ruby
Person.create(:first_name => 'Adam', :last_name => 'Smith')
```

It it nevertheless preferable to use one line per option to facilitate reading
and manipulating options

```ruby
Person.create(:first_name => 'John', #'Adam',
              :last_name  => 'Smith')
```


### Use _one item per line_ when a list items exceeds 80 characters

From the 80 character per line rule

#### Good

```ruby
  attr_accessible :first_name,
                  :last_name,
                  :email,
                  :password,
                  :phone,
                  :address,
                  :city,
                  :password_confirmation,
                  :state,
                  :country
```

#### Better

When the ordering of options is equivalent, favor lexicographical order

```ruby
  attr_accessible :address,
                  :city,
                  :country,
                  :email,
                  :first_name,
                  :last_name,
                  :password,
                  :password_confirmation,
                  :phone,
                  :state
```

#### Not as good

It's tempting to place as many options per line as possible. Don't. It makes it
a lot more convenient to remove, add, and read options when there is only one
per line. Remember, we are not printing screens on paper, and clean code can be
read on digital screens.

```ruby
  attr_accessible :first_name, :last_name, :email, :password,
                  :password_confirmation, :phone, :address, :city, :state,
                  :country
```

#### Bad

In this list

```ruby
  attr_accessible :first_name, :last_name, :email, :password, :password_confirmation, :phone, :address, :city, :state, :country
```

how many attributes are accessible?

Even worse, perhaps, is multiline over 80 characters

```ruby
  attr_accessible :first_name, :last_name, :email, :password, :password_confirmation, :phone, :address, :city, :state,
                  :country
```

### Good

In highly indented position, place the first option on the second line

```ruby
class Reason

  def create
    if person.think?
      Philosopher.create(
        :first_name     => 'Adam',
        :last_name      => 'Smith',
        :occupation     => 'Philosopher',
        :date_of_birth  => '1723-06-23',
        :karma          => 17900717,
        :email          => 'adam.smith@example.com'
      )
    else
      Philosopher.destroy_all
    end
  end

end
```

### _Align delimeters vertically_ on multiline statements

#### Good


```ruby
Person.create(:first_name     => 'Adam',
              :last_name      => 'Smith',
              :occupation     => 'Philosopher',
              :date_of_birth  => '1723-06-23',
              :karma          => 17900717,
              :email          => 'adam.smith@example.com')
```

#### Bad

```ruby
Person.create(:first_name => 'Adam',
              :last_name => 'Smith',
              :occupation => 'Philosopher',
              :date_of_birth => '1723-06-23',
              :karma => 17900717,
              :email => 'adam.smith@example.com')
```

```ruby
Person.create(:first_name => 'Adam',
            :last_name => 'Smith',
            :occupation => 'Philosopher',
            :date_of_birth => '1723-06-23',
            :karma => 17900717,
            :email => 'adam.smith@example.com')
```

#### Bad

Also make sure to left-align options

```ruby
Person.create(:first_name       => 'Adam', # This option aligns to the left of
                                           # subsequent options
                :last_name      => 'Smith',
                :occupation     => 'Philosopher',
                :date_of_birth  => '1723-06-23',
                :karma          => 17900717,
                :email          => 'adam.smith@example.com')
```

### Leave _no whitespace_ at the end of any line

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


### Always use _2 space indentation_


#### Good

```ruby
class Person
  def name
    first_name + ' ' + last_name
  end
end
```

#### Bad

Here's an example with 4 space indentation

```ruby
class Person
    def name
        first_name + ' ' + last_name
    end
end
```


### _No tabs_, ever

### Use _spaces around operators_

#### Good

```ruby
2 + 4
'my' + ' ' + 'space'
@foo ||= 'bar'
```

#### Bad

```ruby
2+4
'my'+' '+'space'
@foo||='bar'
```

### Use _spaces after commas_

#### Good

```ruby
def sum(a, b)
  a + b
end

elements = [1, 2, 3, 21, 45]
```

#### Bad

```ruby
def sum(a,b)
  a + b
end

elements = [1,2,3,21,45]
```

### Use _space after colons_

### _No semicolons_

### Use spaced around { and before }

### No spaces after `(` and before `)`

### Optional spaces after `[` and before `]`

* Use two spaces before statement modifiers (postfix
  if/unless/while/until/rescue).

* Indent when as deep as case.

* Use an empty line before the return value of a method (unless it
  only has one line), and an empty line between defs.

* Use RDoc and its conventions for API documentation.  Don't put an
  empty line between the comment block and the def.

* Use empty lines to break up a long method into logical paragraphs.

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
1.upto(10).select { |n| n % 2 == 1 }
```

#### Not as good

```ruby
1.upto(10).select do |n|
  n % 2 == 1
end
```

#### Bad

Avoid placing `do...end` on the same line

```ruby
1.upto(10).select do |n| n % 2 == 1 end
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

It's not as readable to omit the space before `{`

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

Encoding
--------

### Use Unix-style line endings

* Use ASCII (or UTF-8, if you have to)

Credits
-------

Based largely on [Christian Neukirchen](http://chneukirchen.org/blog/)'s [Ruby Style Guide](https://github.com/chneukirchen/styleguide).

### Contributors

* [olauzon](https://github.com/olauzon/styleguide)
* [theIV](https://github.com/theIV/styleguide)
