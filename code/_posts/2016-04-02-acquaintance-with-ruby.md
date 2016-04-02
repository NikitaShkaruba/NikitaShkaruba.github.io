---
title: "Acquaintance with Ruby"
ref: acquaintance-with-ruby
layout: post
lang: en
---

Hello, today i want to talk about Ruby - high level programming language, which is required on my proposed job.
At the beginning i want to say that Ruby was written so programmers could love to write Ruby code,
so they'll never repeat single wrote line of code,
so lanuage will not contain any surprises like C++.

### Why learn Ruby?
After you learn Ruby and Ruby on rails, you can get a job - ~~laboratory work solver~~ Ruby on Rails developer.
Ruby on rails is a framework for writing web-applications with databases.

### Ruby compared to C/C++ and Java
* Amazing iterators!
* Embedded regular expressions!
* Ranges!
* Block mechanizm - lambda's content!
* Fewer repeated code! Simplified bean(common classes) writing!
* A lof of syntax shugar!
* Strong OOP!
* Every executed line of code returns smething!
* Security, embeeded in language!
* Real good potential of dinamic code execution! In Ruby we can extend the class, methods definitions, change variable scopes, dynamically!

### Ruby features
* It's a compiled and then interpreted language. If we use it as scripting language, it's only interpreted
* Has a Garbage Collector
* Strong duck typization. If we want to create a variable, we don't explicitly specify the type.
* Functions are First Class Objects! We can store functions in variables.
* All variables are just pointers to the real objects on heap.

### Some syntax sugar i do really like
Common iteration of somehting: (Handy replacement of "for", "while" in Java)

```Ruby
3.times do
  print "hi! "
end

# output: hi! hi! hi!
```

Swap - oneliner:

```Ruby
def swap
  a, b = b, a
end
```

Case in Ruby - just a miracle, it can do a lot.

```Ruby
case inputLine

  when "debug"
    dumpDebugInfo
    dumpSymbols

  when /p\s+(\w+)/  
    dumpVariable($1)

  when "quit", "exit"
    exit

  else
    print "Illegal command: #{inputLine}"
end
```

Simple bean, so common used in JavaEE

```Ruby
class simpleBean
  attr_reader :property1, :property2

  def initialize
    @objectField = rand 10
    @@classField = rand 100
  end

  def method1
      @objectField = rand 10
  end
end
```

### Object-Oriented Programming
Ruby - is true OOP language. Everything in ruby is object.
Even methods without explicitly specified class are just methods of global anonymous class

Every literal or constant - object and has methods

```Ruby
num = -1.abs
```

We can even change class-objects.
Composing of class dynamically:

```Ruby
class MediaPlayer
  include Tracing if $DEBUGGING

  if ::EXPORT_VERSION
    def decrypt(stream)
      raise "Decryption not available"
    end
  else
    def decrypt(stream)
      # ...
    end
  end

  def methodB
    # ..
    private: methodB
  end

  def freeze
    # so handy
    self.freeze
  end
end
```

Factory-class:

```Ruby
def factory(klass, *args)
  klass.new(*args)
end

factory(String, "Hello")	»	"Hello"
factory(Dir,    ".")	»	#<Dir:0x401b51bc>

flag = true
(flag ? Array : Hash)[1, 2, 3, 4]	»	[1, 2, 3, 4]
flag = false
(flag ? Array : Hash)[1, 2, 3, 4]	»	{1=>2, 3=>4}
```

### Iterators
Integers provides some really handy iterators, which are a replacement of "for" loop in C-like languages

```Ruby
3.times        { print "X " }
1.upto(5)      { |i| print i, " " }
99.downto(95)  { |i| print i, " " }
50.step(80, 5) { |i| print i, " " }

# output: X X X 1 2 3 4 5 99 98 97 96 95 50 55 60 65 70 75 80
```

Integers - not only constants, even variables!

```Ruby
num = rand 10
num.times do
  print "It's working!"
end

# output: It's working!It's working!
```

Collection iteration

```Ruby
[ 1, 1, 2, 3, 5 ].each {|val| print val, " " }
```

### Standard types
Integer in Ruby can be any length!
Little(size < machine word - 1 bit) integers are stored at fixnum objects
Big(size >= machine word - 1 bit) are stored in Bugnum(managed sequence of fixnums)
Execution environment converts them by herself, we don't need to do something.

```Ruby
num = 8
7.times do
  print num.type, " ", num, "\n"
  num *= num
end

# output:
# Fixnum 8
# Fixnum 64
# Fixnum 4096
# Fixnum 16777216
# Bignum 281474976710656
# Bignum 79228162514264337593543950336
# Bignum 6277101735386680763835789423207666416102355444464034512896
```

Float in Ruby is stored in native float-word
String in Ruby is just a sequence of bytes, objects with type String

Arrays in Ruby can contain various types together.

```Ruby
a = [ 3.14159, "pie", 99 ]
a.type	   # »	Array
a.length	 # »	3

a[0]	     # »	3.14159
a[1]	     # »	"pie"
a[2]	     # »	99
a[3]	     # »	nil
```

Hashes in Ruby - really handy type, which we can instantinate beautifully.

```Ruby
hash = {
  "Winter" -> "Snow Fights",
  "Summer" -> "Swimming",
  "Autumn" -> "Night walks",
  "Spring" -> "Day walks"
}
```

### Ranges
Ranges in Ruby - independent type. There are 2 operators to work with ranges.
The two-period ".." form includes the end position, while the three-period "..." form does not.

```Ruby
1..4      # > 1, 2, 3, 4
1...4     # > 1, 2, 3
'a'..'z'  # > 'a', 'b', .. , 'y', 'z'

# Type convertion. Range - stanalone type!
('foo'..'foq').to_a > ['foo', 'fop', 'foq']
```

### How to easy create a compared type!
In Ruby there is so-called spaceship-operator "<=>", and also mixin Comparable, which declares all the other comparisson operation via spaceship-operator

```Ruby
class Man
  # include all methods from interface
  include Comparable

  def initialize
    @health, @perseverance, @charisma, = 3.times.collect { rand 10 }
  end  

  def <=>(other)
    if self.health < other.health && self.perseverance < other.perseverance && self.charisma < other.charisma then -1
    if self.health > other.health && self.perseverance > other.perseverance && self.charisma > other.charisma then 1
    else 0 # Mens are equal if their attributes vary, because we can argue to the end of the world.
  end
end
```

### Built-in Regular expressions
Ruby has Regular expressions because it's author - Yukihiro Matsumoto did liked Perl. I'll write a separate article about them.

### Blocks
Blocks are an executed code lines, which are the content of lambdas or methods. They are widely used in Ruby's standart library

Did you ever traversed a tree, or realized pattern Visitor? In Ruby it's so easy!  
Example where we provide with block what to do with computed number.

```Ruby
def fibonacciUpTo(max)
  i1, i2 = 1, 1    
  while i1 <= max
    yield i1
    i1, i2 = i2, i1+i2
  end
end

fibonacciUpTo(1000) { |f| print f, " " }

# output: 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
```

Yield can be not single, and also he can have parameters!

```Ruby
def callBlock
  yield 0
  yield 1
end

callBlock { |i| puts "In the block" + i }

# output:
# In the block
# In the block
```

### Returned values
In RUby every executed line of code returns something, so we can omit return statement

```Ruby
def pow number, power
  number ** power
end
```

That makes it so easy to write so-called trailing-expressions.

```Ruby
class Popper
  def initialize(size)
    @array = size.times.collect { rand 100 }
  end

  def pop(amount)
    @array.pop
    self # return himself
  end
end

popper = Popper.new(6)
popper.pop(3).pop(2).pop(1)
```

### Reflection
Ruby fully supports reflection, like in any other high-level languages

### Security
Ruby has $SAFE gloval variable for every thread, so we can define Ruby-paranoia level (from 1 to 4)

Usage:

```Ruby
f=open(fileName,"w")
f.print ...   # write untrusted program into file.
f.close

Thread.start {
  $SAFE = 4
  load(fileName, true)
}
```

#### $SAFE levels
Just so live in out world is so dnagerous, there is full description of $SAFE levels

*$SAFE >= 1*
The environment variables RUBYLIB and RUBYOPT are not processed, and the current directory is not added to the path.
The command-line options -e, -i, -I, -r, -s, -S, and -x are not allowed.
Can't start processes from $PATH if any directory in it is world-writable.
Can't manipulate or chroot to a directory whose name is a tainted string.
Can't glob tainted strings.
Can't eval tainted strings.
Can't load or require a file whose name is a tainted string.
Can't manipulate or query the status of a file or pipe whose name is a tainted string.
Can't execute a system command or exec a program from a tainted string.
Can't pass trap a tainted string.

*$SAFE >= 2*
Can't change, make, or remove directories, or use chroot.
Can't load a file from a world-writable directory.
Can't load a file from a tainted filename starting with ~.
Can't use File#chmod , File#chown , File#lstat , File.stat , File#truncate , File.umask , File#flock , IO#ioctl , IO#stat , Kernel#fork , Kernel#syscall , Kernel#trap . Process::setpgid , Process::setsid , Process::setpriority , or Process::egid= .
Can't handle signals using trap.

*$SAFE >= 3*
All objects are created tainted.
Can't untaint objects.

*$SAFE >= 4*
Can't modify a nontainted array, hash, or string.
Can't modify a global variable.
Can't access instance variables of nontainted objects.
Can't change an environment variable.
Can't close or reopen nontainted files.
Can't freeze nontainted objects.
Can't change visibility of methods (private/public/protected).
Can't make an alias in a nontainted class or module.
Can't get meta information (such as method or variable lists).
Can't define, redefine, remove, or undef a method in a nontainted class or module.
Can't modify Object.
Can't remove instance variables or constants from nontainted objects.
Can't manipulate threads, terminate a thread other than the current, or set abort_on_exception.
Can't have thread local variables.
Can't raise an exception in a thread with a lower $SAFE value.
Can't move threads between ThreadGroups.
Can't invoke exit, exit!, or abort.
Can load only wrapped files, and can't include modules in nontainted classes and modules.
Can't convert symbol identifiers to object references.
Can't write to files or pipes.
Can't use autoload.
Can't taint objects.

Any Ruby object derived from some external source (for example, a string read from a file, or an environment variable)
is automatically marked as being tainted. If your program uses a tainted object to derive a new object, then
that new object will also be tainted, as shown in the code below. Any object with external data somewhere in its
past will be tainted. This tainting process is performed regardless of the current safe level.
You can inspect the tainted status of an object using Object#tainted?

```Ruby
# Internal data
x1 = "a string"
x1.tainted?	»	false
x2 = x1[2, 4]
x2.tainted?	»	false
x1 =~ /([a-z])/	»	0
$1.tainted?	»	false

# External data
y1 = ENV["HOME"]
y1.tainted?	»	true
y2 = y1[2, 4]
y2.tainted?	»	true
y1 =~ /([a-z])/	»	1
$1.tainted? » true

# Taint untaint usage
x1 = "a string"
x1.tainted?	»	false
x1.taint
x1.tainted?	»	true
x1.untaint
x1.tainted?	»	false
```

### Performance
I will compare ruby's performance with C, Java, Python and PHP. Proofs are [here](http://benchmarksgame.alioth.debian.org/)

* Ruby 1.9 vs. Python3 within the same order of magnitude
* Ruby 1.9 vs. PHP within the same order of magnitude
* Ruby 1.9 vs. Java 6 server up to two orders of magnitude slower!
* Ruby 1.9 vs. C (gcc) up to two orders of magnitude slower!

But we don't need fast performance for web-development, we need to write code fast, and have it in good readability.
Ruby was created with this phrase in mind.

### Afterword
So, that was a brief overview of this wonderful language! Wonderful - because after i wrote my first enterprise project in JavaEE,
i was highly dissapointed of this language. I knew that my code is a bit tangled, and that was because of the language realization.
But Ruby is different, it's just slower, alright? My code is so fabulous and i really like it.

But the most nice thing about Ruby is the Ruby in Rails web-framework. I'll write my next article about it in my next post.

Hey, see you :smile: And stay awesome, my reader! :wink:
