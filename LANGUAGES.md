

#### Ruby: `mixins`
acole

Modules => Mixins

Modules are a way of grouping together methods, classes, and constants. Modules give you two major benefits:

1. Modules provide a namespace and prevent name clashes.
2. Modules implement the mixin facility.

Namspaces

Often your code will be organized into classes, so you'll probably stick a class (or a set of interrelated classes) into a file.
However, there are times when you want to group things together that don't naturally form a class.

The answer is the module mechanism. Modules define a namespace, a sandbox in which your methods and constants can play without having to worry about being stepped on by other methods and constants. The trig functions can go into one module:

```
module Trig
  PI = 3.141592654
  def Trig.sin(x)
   # ..
  end
  def Trig.cos(x)
   # ..
  end
end
```

Module constants are named just like class constants, with an initial uppercase letter. The method definitions look similar, too: these module methods are defined just like class methods.

As with class methods, you call a module method by preceding its name with the module's name and a period, and you reference a constant using the module name and two colons.

Modules have another, wonderful use. At a stroke, they pretty much eliminate the need for multiple inheritance, providing a facility called a mixin.

A module can't have instances, because a module isn't a class. However, you can include a module within a class definition. When this happens, all the module's instance methods are suddenly available as methods in the class as well. They get mixed in. In fact, mixed-in modules effectively behave as superclasses.

```
module Debug
  def whoAmI?
    "#{self.type.name} (\##{self.id}): #{self.to_s}"
  end
end
class Phonograph
  include Debug
  # ...
end
class EightTrack
  include Debug
  # ...
end
ph = Phonograph.new("West End Blues")
et = EightTrack.new("Surrealistic Pillow")
ph.whoAmI?	»	"Phonograph (#537766170): West End Blues"
et.whoAmI?	»	"EightTrack (#537765860): Surrealistic Pillow"
```

Mixins give you a wonderfully controlled way of adding functionality to classes. However, their true power comes out when the code in the mixin starts to interact with code in the class that uses it. Let's take the standard Ruby mixin Comparable as an example. The Comparable mixin can be used to add the comparison operators (<, <=, ==, >=, and >), as well as the method between?, to a class. For this to work, Comparable assumes that any class that uses it defines the operator <=>. So, as a class writer, you define the one method, <=>, include Comparable, and get six comparison functions for free. Let's try this with our Song class, by making the songs comparable based on their duration. All we have to do is include the Comparable module and implement the comparison operator <=>.

```
class Song
  include Comparable
  def <=>(other)
    self.duration <=> other.duration
  end
end
```

```
song1 = Song.new("My Way",  "Sinatra", 225)
song2 = Song.new("Bicylops", "Fleck",  260)
song1 <=> song2	»	-1
song1  <  song2	»	true
song1 ==  song1	»	true
song1  >  song2
```
--

#### Ruby: `classes` `inheritance`
kgrosh

#Classes in Ruby
Creating classes in Ruby is very easy to do, you must start with the keyword 'class' and follow it with the name of the class and then the class definition is completed with an 'end' keyword.
```ruby
class Mammal
end

theMan = Mammal.new
```
This code would define a Mammal class and we make an object called theMan which is an instance of the Mammal class we just defined.

Let's add some properties to the Class so that it looks more like something that we would actually use..

```ruby
class Mammal
	@@numMammals = 0
	def initialize(name, type)
		@mammalName = name
		@mammalType = type
	end
end

theMan = Mammal.new("Konrad","Human")
```
The initialize method is a special type of method, which will be executed when the new method of the class is called with parameters.
Using the class variable @@numMammals, you can determine the population of mammals that are created.

I learned about classes in Ruby at <a href="http://www.tutorialspoint.com/ruby/ruby_classes.htm"target="_blank">tutorialspoint.com/ruby</a>

#Inheritance in Ruby
In Ruby, a class can only inherit from a single other class. Other languages allow for inheritance from multiple classes, but Ruby doesn't.
Below is an example of a basic example of Inheritance.

```ruby
class Mammal  
  def breathe  
    puts "inhale and exhale"  
  end  
end  
  
class Cat < Mammal  
  def speak  
    puts "Meow"  
  end  
end  
  
rani = Cat.new  
rani.breathe  
rani.speak
```
Source: <a href="http://rubylearning.com/satishtalim/ruby_inheritance.html"target="_blank">rubylearning.com</a>


Note the line where the class definition for cat is 'class Cat < Mammal'  the < operator is used to show the inheritance. The cat inherited the ability to breathe, which can be fairly useful.

There are certain times when a subclass doesn't want to inherit all of the properties of the class it's inheriting from. 

```ruby
class Bird  
  def preen  
    puts "I am cleaning my feathers."  
  end  
  def fly  
    puts "I am flying."  
  end  
end  
  
class Penguin < Bird  
  def fly  
    puts "Sorry. I'd rather swim."  
  end  
end  
  
p = Penguin.new  
p.preen  
p.fly
```
Source: <a href="http://rubylearning.com/satishtalim/ruby_inheritance.html"target="_blank">http://rubylearning.com/satishtalim/ruby_inheritance.html</a>


---

#### Ruby: `numbers` `arithmetic`
arthurfc

---

#### Ruby: `blocks` &amp; `collections`
mthurmon

part 0.
---

#### Ruby: `data types` &amp; `symbols`
zlambert

herp derp

---

#### Ruby: `modules`
yyang
Introduction 
Ruby was invented in 1993 by Yukihiro Matsumoto. It is open source with subject to a license. Ruby is object-oriented 
and interpreted language which has a clean and easy syntax. The programming is popular because it is scalable and easy to maintain. 

Module is an important feature of the Ruby programming language. It supports multiple inheritances indirectly, and is a major 
object-oriented feature of the language. Modules group together methods, classes and constants. Modules are defined much like classes, 
but the module keyword is used in place of the class keyword. There are two main advantages of modules:

1. Modules provide a namespace which prevents name clashes;
2. Modules implement the mixin feature.

Namespace is a way of grouping logically related objects together. This allows classes or modules with same names to co-exist without clashes. 
Think of this as storing different files with the same names under separate directories in the file system.

Syntax and Semantics

The syntax of modules looks like:
```
module Identifier
   statement1
   statement2
   ...........
end
```

And here is a simple example of module:

```
#!/usr/bin/ruby
#Module defined in Area.rb file
module Area
   PI = 3.141592654               #module constant
   def Area.round(r)              #module method
   # ..
   end
   def Area.sphere(r)             #module method
   # ..
   end
end
```

The constants of Module are named similar to the class constants with an uppercase letter. The methods of module are defined in the same way 
as class methods. Below is an example of modules, which has a constant PI and two module methods. We call the module method by preceding the 
method’s name with the module’s name and a period, e.g. Area.round(r) . To access constants, we call the module constant using the module name, 
two colons, and the constant name. e.g. Area::PI.

When & How Modules are Used?

1. Namespaces
When we work on big Ruby program, we usually write more than one class with logically related functions grouped in a file rather than put everything 
in one class.  And then we import/include the relevant classes into a file if we need to use the classes in the file. However, there is a risk when the 
classes contain functions with the same name. Say Molly writes a file called area.rb, and defines functions to calculate the area of square, round, 
sphere and etc. Mick worked on shape.rb class to determine the shape. You want to write a ruby program to determine the shape and then calculate the area. 
So I include both area.rb and shape.rb to my program, and both of the classes defined a round method. The program will be confused to choose the 
appropriate method.

The way to solve the namespace conflicts problem is using module mechanism.  Below is an example of how to use modules in Ruby. The first block defines 
a module named Area, and has two methods Area.round(r) and Area.sphere(r) which is in Area.rb file. The second block defines a module named Shape with two methods,
Shape.round(yesorno) and Shape.sphere(yesorno).  The modules on the first and second file have the round and sphere functions.

```
#!/usr/bin/ruby
#Module defined in Area.rb file
module Area
   PI = 3.141592654               #module constant
   def Area.round(r)              #module method
   # ..
   end
   def Area.sphere(r)             #module method
   # ..
   end
end
```

```
#!/usr/bin/ruby
#Module defined in Shape.rb file
module Shape
   YES =1
   NO = 0
   def Shape.round(yesorno)
   # ...
   end
   def Shape.sphere(yesorno)
   # ...
   end
end
```

If a third program wants to use these modules, it can simply load the two files using the Ruby require statement, and reference the qualified names. 
The Ruby require statement is similar to the import statement of Java and the include statement of C and C++. It does not matter using require “area.rb” or require “area.”
```
require “area.rb”
require “shape”

x = Area.round(1)
fact = Shape.round(Shape::YES)
```
Using modules, the program will know which function to use which will avoid names conflicting problem.

2. Mixin
(Another student did this part, so I won't talk thorougly on mixin.)
Like Java, Ruby does not support multiple inheritances directly. However, Ruby Modules can solve the problem by adding functionality to classes. 
In the namespace section, we defined module methods whose names are prefixed by the module name. There is another way to define methods in modules 
without prefixing of module name. 
In the previous section's examples, we defined module methods, methods whose names were prefixed by the module name. If this made you think of class methods, 
your next thought might well be “what happens if I define instance methods within a module?” Good question. A module can't have instances, because a module isn't a class. 
However, you can include a module within a class definition. When this happens, all the module's instance methods are suddenly available as methods in the class as well. 
They get mixed in. In fact, mixed-in modules effectively behave as superclasses.

Problem
Modules are part of what makes Ruby’s design beautiful. However, since they do not have a direct analogy in any mainstream programming language, it is easy to get a bit confused about what they should be used for.

Conclusion

---

#### Ruby: `scope`
jdelagar

---

#### Ruby: `duck typing`
lmatsind


Intro:

Ruby is a dynamic, open source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.
Every procedure in Ruby is a method of some object. Some method calls appear to be function calls as in other languages, but in fact they are actually invocations of methods belonging to self. Parentheses can be omitted if unambiguous.
Ruby is a dynamic, reflective, object-oriented, general-purpose programming language. It was designed and developed in the mid-1990s by Yukihiro "Matz" Matsumoto in Japan.

Meat:

Ruby’s dynamic nature facilitates a style of type system known as duck typing. In particular, duck typing breaks the strong association between an object’s class and its type by defining types based on what an object can do rather than what class it was born from.

My favorite example:

```
class Duck  
  def quack  
    'Quack!'  
  end  
  
  def swim  
    'Paddle paddle paddle...'  
  end  
end  
  
class Goose  
  def honk  
    'Honk!'  
  end  
  def swim  
    'Splash splash splash...'  
  end  
end  
  
class DuckRecording  
  def quack  
    play  
end  
  
  def play  
    'Quack!'  
  end  
end  
  
def make_it_quack(duck)  
  duck.quack  
end  
puts make_it_quack(Duck.new)  
puts make_it_quack(DuckRecording.new)  
  
def make_it_swim(duck)  
  duck.swim  
end  
puts make_it_swim(Duck.new)  
puts make_it_swim(Goose.new)  
```

If you refer to the code shown below:

```
def make_it_quack(duck)  
  duck.quack  
end  
puts make_it_quack(Duck.new)  
puts make_it_quack(DuckRecording.new)  
```

A method that told a Duck to quack works when given a DuckRecoding, due to Duck Typing. Similarly in the following code:
```
def make_it_swim(duck)  
  duck.swim  
end  
puts make_it_swim(Duck.new)  
puts make_it_swim(Goose.new)  
```
A method that tells a Duck to swim when given a Goose, works.

Duck typing to avoid scope creep

```
def image(file, options={})
  Prawn.verify_options [:at, :position, :vposition, :height,
                        :width, :scale, :fit], options

  if file.respond_to?(:read)
    image_content = file.read
  else
    raise ArgumentError, "#{file} not found" unless File.file?(file)
    image_content = File.binread(file)
  end

  # additional implementation details omitted.
end
```

The above code is used to make it so that the image() method can be called with either a file name or a file handle

Some more examples

```
class Duck
  def quack
    puts "Quaaaaaack!"
  end
 
  def feathers
    puts "The duck has white and gray feathers."
  end
end
 
class Person
  def quack
    puts "The person imitates a duck."
  end
 
  def feathers
    puts "The person takes a feather from the ground and shows it."
  end
end
 
def in_the_forest(duck)
  duck.quack
  duck.feathers
end
 
def game
  donald = Duck.new
  john = Person.new
  in_the_forest donald
  in_the_forest john
end
game
```

Output:

Quaaaaaack!
The duck has white and gray feathers.
The person imitates a duck.
The person takes a feather from the ground and shows it.


In Ruby, we rely less on the type (or class) of an object and more on its capabilities. Hence, Duck Typing means an object type is defined by what it can do, not by what it is. Duck Typing refers to the tendency of Ruby to be less concerned with the class of an object and more concerned with what methods can be called on it and what operations can be performed on it. In Ruby, we would use respond_to? or might simply pass an object to a method and know that an exception will be raised if it is used inappropriately.

```
# Check in irb, whether the object defines the to_str method  
>> 'A string'.respond_to?(:to str)  
=> true  
>> Exception.new.respond_to?(:to_str)  
=> false  
>> 4.respond_to?(:to_str)  
=> false  
```

The example above is the simplest example of Ruby's philosophy of "duck typing:" if an object quacks like a duck (or acts like a string), just go ahead and treat it as a duck (or a string). Whenever possible, you should treat objects according to the methods they define rather than the classes from which they inherit or the modules they include.

Outro:

Duck Typing Pro’s
i)  Convenient
ii) Promotes code reuse
    All that matters is what messages an object can receive
 
Duck Typing Con’s
i) “Obvious” equivalences don’t hold: x+x, 2*x, x*2
ii) May expose more about an object than might be
    desirable (more coupling in code)


---

#### Ruby: `method_missing` &amp; `const_missing`
dmesenbr

part 0 lol ermagerhd!

---

#### Ruby: `IO` `files`
cnelson

---

#### Go: `goroutines`
mclausen

<<<<<<< HEAD
---
<<<<<<< HEAD

#### Scala: `pattern matching` 
btombari

Scala is a programming language which uses the JVM
Scala is very similar to Java, but is a fully functional language and also contains additional features
Pattern matching in Scala is structured like a switch-case statement in Java.
	-
```
object Example1 {
	def main(args: Array[String]) {
		println(patternMatch(3))
	}
	def patternMatch(x: Int) : String = x match {
		case 1 => "One"
		case 2 => "Two"
		case 3 => "Three"
		case 4 => "Four"
		case 5 => "Five"
		case 6 => "Six"
		case 7 => "Seven"
		case 8 => "Eight"
		case 9 => "Nine"
		case _ => "Not A Number"
	}
}
```

The => operator separates the pattern from the expression.
The matched case will return the expression.
Underscore serves as the default for any pattern which does not fit the cases above it(primitive data types).
Scala calls toString and equals methods automatically.
Scala allows or using arbitrary data types in pattern matching

```
object Example2 {
	def main(args: Array[String]) {
		val johnS = new Person("John", "Smith")
		val JohnD = new Person("John", "Davis")
		
		for(person <- list(johnS, johnD)) {
			person match {
				case Person("John", "Smith") => println("True")
				case Person(First, Last) => println("Unknown person " + First + " " + Last)
			}
		}
	}
	case class Person(First: String, Last: String)
}
```
=======
=======
#### 'Enumerations' and 'Subscripts'
ncabral

##### Enumerations

Like in other languages, enumerations in Swift allow the programmer to define a common type for a group of related values. Enumerations are used when the programmer wants to work with user defined values in a type-safe way. Unlike languages such as C, enumerations in Swift do not have an implied "raw" value (0, 1, 2, etc). Rather, the members are treated as values of specific type. However, the programmer can still associate specific values of any type along with each member if they choose to. Enumerations are first class types in Swift, and they can have computed properties as well as instance methods.

The best practice when defining an enumeration is to capitalize the name, since an enumeration is a type. It is also preferable that enumeration names are singular.

One common mistake when using enumerations in Swift is assuming that each member has an implied numerical, like they do in C. It is important to remember that each member is a value in and of itself, of the type specified by the name of the enumeration.

The following code sample shows a couple of ways to define an enumeration:
```
enum Directions{
	case Up
	case Down
	case Left
	case Right
}

enum Taste{
	case Sweet, Sour, Bitter, Salty, Umami
}
```
A variable's type is inferred when it is initialized to one of the possible values of an enumeration. It can then be reassigned to another value of that enumeration using a shorter dot syntax, as seen in the following code example:
```
	var foodTaste = Taste.Bitter
	foodTaste = .Sour
```
##### Subscripts

Subscripts in Swift are a shortcut for accessing the member elements of a collection. This allows the programmer to set and get values by index without the need for seperate methods. Subscripts can also be overloaded, in which case the correct subscript is called based on the index value that is passed.

Subscripts are defined with the subscript keyword. They have a specific index value type, as well as a specific return type. The programmer has the option to make the subscript read/write or read-only. The following code example shows both types of subscript. Note that the example is an overloaded subscript.

```
subscript(index: Int) -> Int {
	get {
		//returns a type specified in line 1
	}
	set(newValue) {
		// note that newValue is of this same type
	}
}

subscript(index: String) -> Int {
	get {
		// returns a var of type Int
	}
}
```
The following code example shows subscript usage. Note that this example does not use the example code seen above.
```
var myNumbers = ["one":1, "two":2, "three":3]
myNumbers["four"] = 4
var myVar = myNumbers["one"] //myVar now equals 1
```

##### Sources
<a href="https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Enumerations.html">Apple Developer Website - Enumerations</a>

<a href="https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Subscripts.html">Apple Developer Website - Subscripts</a>

>>>>>>> 008e5a7aa827e36f6bf483ae199789dac5a459b2
#### Swift: `Control Flow Structures` and `Exception\Error Handling`
mtaylor

##### Control Flow Structures:
Swift uses the same famliar control flow statements from modern programming languages.

Most common ones are: for-in, for, if, case

<a href=http://swiftstub.com/805263090/>For-in Loop</a href>

```
for i in 0...10 {
    println("\(i) times 7 is \(i * 7)")
}

Output is:
0 times 7 is 0
1 times 7 is 7
2 times 7 is 14
3 times 7 is 21
4 times 7 is 28
5 times 7 is 35
6 times 7 is 42
7 times 7 is 49
8 times 7 is 56
9 times 7 is 63
10 times 7 is 70
```

<a href=http://swiftstub.com/539183439/>For Loop</a href>

```
for var i = 1; i <= 10; i++ {
    println("Iteration: \(i)")
}

Output is:
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
Iteration: 5
Iteration: 6
Iteration: 7
Iteration: 8
Iteration: 9
Iteration: 10
```

<a href=http://swiftstub.com/739944485/>If Statements</a href>

```
var drinkingAge = 21
var age = 19
if age >= drinkingAge {
     println("You may buy alcohol because you are \(age)")
} else {
    println("You may not buy alcohol because \(age) is underage")
}

Output is:
You may not buy alcohol because 19 is underage
```

<a href=http://swiftstub.com/473864834/>Case Statements</a href>

```
let count = 25
let str = "types of twisty puzzles"
var incrementalCount: String
switch count {
case 0:
    incrementalCount = "no"
case 1...3:
    incrementalCount = "a few"
case 4...9:
    incrementalCount = "several"
case 10...99:
    incrementalCount = "tens of"
case 100...999:
    incrementalCount = "hundreds of"
case 1000...999_999:
    incrementalCount = "thousands of"
default:
    incrementalCount = "millions and millions of"
}
println("There are \(incrementalCount) \(str).")

Output is:
Matt owns tens of types of twisty puzzles.
```

##### Exception\Error Handling:

Runtime errors:

As someone on StackOverFlow suggests: "for handling runtime errors (like network connectivity problems, parsing data, opening file, etc) you should use NSError like you did in ObjC, because the Foundation, AppKit, UIKit, etc report their errors in this way. So it's more framework thing than language thing."

In addition he said that: "Another frequent pattern that is being used are separator success/failure blocks like in AFNetworking:"

```
var sessionManager = AFHTTPSessionManager(baseURL: NSURL(string: "yavin4.yavin.planets"))
sessionManager.HEAD("/api/destoryDeathStar", parameters: xwingSquad,
    success: { (NSURLSessionDataTask) -> Void in
        println("Success")
    },
    failure:{ (NSURLSessionDataTask, NSError) -> Void in
        println("Failure")
    })
Still the failure block frequently received NSError instance, describing the error.
```

Programmer errors:

For programmer errors (like out of bounds access of array element, invalid arguments passed to a function call, etc) you used exceptions in ObjC. Swift language does not seem to have any language support for exceptions (like throw, catch, etc keyword). However, as documentation suggests it is running on the same runtime as ObjC, and therefore you are still able to throw NSExceptions like this:

```
NSException(name: "SomeName", reason: "SomeReason", userInfo: nil).raise()
```
You cannot catch them in pure Swift, so you have to opt for catching exceptions in ObjC code.
>>>>>>> f8e8a3c867648d01d3985a52b9fda6688fa4fc28

---

#### Scala: `classes` &amp; `traits`
sodham

---

#### Swift: `enumerations` &amp; `subscripts`
ncabral

test

---

#### Swift: `control flow structures` &amp; `exception/error handling`
mtaylor, 

---

#### Swift: `typing system`
types, nested types, generics
jpeng

---

#### Dart: `Libraries` &amp; `Visibility`
tfogdall

#####Libraries
The phrase "batteries included" is used frequently throughout Google's
documentation at <a href="http://www.dartlang.org"
target="_blank">dartlang.org</a>, and this is probably most evident in their
widely available libraries. Every Dart application is itself a library,
although there are two types, and one is considerably easier to use than the
other. To utilize class and methods from one of the included (and seemingly
more official) Dart libraries that come installed with the Dart SDK, use the
```import``` keyword as shown below. All code snippets taken from <a
href="https://drive.google.com/file/d/0B9psPUqcRKYpN0QtRHdUSUJyQnM/view?usp=sharing"
target="_blank">this program</a> that performs several types of numerical
integration on .csv-formatted bivariate data sets. (A screen shot of <a
href="https://drive.google.com/file/d/0B9psPUqcRKYpbHNzSXRhZ19yMzA/view?usp=sharing"
target="_blank">this program's output using a simply .csv file generated by
LibreOfficeCalc is available here</a>.)

```
import 'dart:io';
import 'dart:collections';
import 'dart:math';
```

#####Packages
In all three above instances, the library is one that is included with the
regular Dart installation. If classes and methods that are define in what the
language designers refer to as a "package," there is a substantial archive of
these libraries available at <a href="http://pub.dartlang.org"
target="_blank">pub.dartlang.org</a>.Packages are installed using the ```pub```
package manager, which can be used to download any of the packages in the
repository. Once downloaded, they can be installed using the ```import```
keyword, though the syntax is a little different. For instance, the
tapo_calendar package is useful for implementing a simple day-view calendar for
<a href="https://www.dartlang.org/polymer" target="_blank">Dart's port of
polymer</a>. Once ```pub``` is used to acquire the package, it can be imported
as follows:
```
import 'package:tapo_calendar/calendarview/calendarview.dart';
import 'package:tapo_calendar/eventlist/eventlist.dart';
```

#####Visibility
As mentioned above, every Dart application is itself a library, and anyone can
publish their library to <a href="http://pub.dartlang.org"
target="_blank">pub.dartlang.org</a>. That said, if one wished to publish their
code to the repository for the purposes of sharing, they may still choose to
make identifiers visible only within the library by adding an underscore to the
identifier. For instance:
```
void _populate() {
   String current;
   List<String> currString;
   int i;
   for(i=0;i<rawData.length;i++) {
     current = rawData.elementAt(i);
     currString = current.split(",");
     xs.add(double.parse(currString.elementAt(0).trim(),null));
     ys.add(double.parse(currString.elementAt(1).trim(),null));
   }
}
```
The above method is visible only within the dart application from above.
Consequently, anyone importing the code for use in their own application would
be unable to use this method.

#####Avoiding Naming Conflicts
In the event that two libraries have elements with the same identifier, the
following can be added to the import statement:
```
import 'package:lib1/ex.dart' as ex1;
import 'package lib2/ex.dart' as ex2;
```
Then, if two elements with the same name are used within the same code, the
following will make clear which is which:
```
Element a = new ex1.Element();
Element b = new ex2.Element();
```

#####Establishing Formal Libraries
As mentioned previously, every application in Dart is a library, even if the
following is not included, but to formally declare one as such, use
```library``` and ```part of```.
```
library numint; //Declare that numint is a library.
```
Once the library is established, additional source files can be included with
the library as follows:
```
part of numint; //Declare that this file is part of the above library.
```

#####General User-Friendliness
Google's goal in creating Dart was to make a user-friendly,
"batteries-included" PL for implementing modern web-based applications. From
this perspective, they have succeeded immensely given how easy it is to include
and utilize code from various libraries. On the other hand, even though the
language runs off of the Java Virtual Machine, several data structures behave
differently than they would in Java, so it takes some time to get over the
learning curve. For instance, in the ```dart:collections``` library, there is a
```LinkedList``` structure that only accepts objects that implement Dart's
```LinkedListEntry``` class. If one wishes to use a data structure that accepts
a generic data type, other structures must be used. The application
```numint.dart``` resorts to using a ```Queue<double>``` data structure to
house the inputs and outputs from the data set.

Other issues that were encountered generally came about because of the weak
typing system that the language uses. One should be aware that it is very easy
to play loose with type-declarations in the code, only to have frequent bugs
pop up if the the declarations are not handled carefully.

---

#### Dart: `classes` &amp; `operator overloading`
cjohnson
# Google Dart

##### Dart is a cohesive, scalable platform for building apps that run on the web (where you can use Polymer) or on servers (such as with Google Cloud Platform). Use the Dart language, libraries, and tools to write anything from simple scripts to full-featured apps.
[Dart Homepage]

##Classes

Similar to Java everything every thing in the Dart language is an object.  Therefore classes are objects and everything is an instance of a class.  Classes provide a modular design to the structure of your program by classifying everything as an instance of the class.  Classes support instance variables, constructors and methods for manipulating and obtaining the instance variables, also known as getters and setters.

**The class shown below will be the class referenced in the following examples.**
```javascript
class Person {
String firstName;
String lastName;

Person(String firstName, {String lastName}) {
this.firstName = firstName;
this.lastName = lastName;
}

@override
String toString() => print('First: $firstName, Last: $lastName');
}
```
###Getters & Setters

Dart provides many shortcuts or "syntactic sugar" for writing less code which also makes the code easier to read.  An example of this is the fat arrow used for writing getters of a class.  In the example shown below the fat arrow '=>' is the same as writing out the code block within brackets "{ return expr; }".
```javascript
String get firstName => firstName;
```
The structure of this get method is first the return type, the method, the name of the method and followed by the body of the getter method.  The method 'get' is special to the Dart class because getters and setters are implicitly implemented in the language.  This is useful for writing far less code in getter methods not needing to do any further computation and only return the instance variable of the class.  With this in mind, when we create a new instance of this class, lets say it is a Person class and we want to obtain the Persons' first name the snippet shown below will actually be the same as the code shown above but is instead done under the hood of the language.
```javascript
Person person = new Person('Chad');
String myName = person.firstName;
```
This same functionality is also available for setter methods used to manipulate the value of the instance variable.  If I wanted to change the last name of my person from 'Johnson' to 'Ochocinco' I can simply use the line of code below to change the name.
```javascript
person.lastName = 'Ochocinco';
```
What this is actually doing is similar to the getter function and implicitly is the same as the function shown below.
```javascript
void set lastName(String newLastName) {
lastName = newLastName;
}
```
###Constructors
Besides manipulating and accessing the variables of a class we also need to create instances of the class.  Instances of a class are created with a constructor and are named after the class itself.  In the Person example we can see the constructor is the method defined called 'Person'.  The 'this' refers to the instance of the class being constructed.  Therefore we are creating a new instance of person with the provided first name and last name.

What you might have noticed is not only the brackets around the parameter lastName, but also that I created a Person object above and did not include the last name.  The brackets around the parameter indicate that this is an optional parameter.  Also, to write even less code Dart has also implemented a shortcut which is the same as the constructor above but much more concise.
```javascript
Person(this.firstName, {this.lastName});
```
If we wanted to create a new instance of Person with a last name the optional parameter is provided as a named parameter to the constructor.  This looks familiar to those who might know Objective-C.  The following lines after creating the new instance will manipulate the specific instance called 'person'.
```javascript
Person person = new Person('Ronald', lastName: 'Artest');
person.firstName = 'Metta';
person.lastName = 'World Peace';
//Output: 'First: Metta, Last: World Peace
```
Finally, for constructors since Dart is an optionally typed language where all arguments to a method are not required a method cannot be overloaded based on its argument types.  This is not an issue for most methods as you can simply name your methods differently, but for constructors you are required to use the name of the class.  There is a feature that will allow you to create multiple constructors though by naming them.  The example below shows a class with two named constructors, 'fromXml' and 'fromJson'.  Each class also has a default constructor that receives no arguments.
```javascript
class FluffyBunny {
FluffyBunny.fromXml(String xml) {
// …
}

FluffyBunny.fromJson(String json) {
// ...
}
}

var xml = "<bunny><name>floppy</name></bunny>";
var json = '{"bunny":{"name":"peter"}}';

var floppy = new FluffyBunny.fromXml(xml);
var peter = new FluffyBunny.fromJson(json);
```

**Factory Constructor**
```javascript
class Symbol {
final String name;
static Map<String, Symbol> _cache;

factory Symbol(String name) {
if (_cache == null) {
_cache = {};
}

if (_cache.containsKey(name)) {
return _cache[name];
} else {
final symbol = new Symbol._internal(name);
_cache[name] = symbol;
return symbol;
}
}

Symbol._internal(this.name);
}
```

##Operator Overloading
Operators in Dart are the same operators as those in most languages but the difference in Dart is these operators can be overwritten.  Similar to overriding the toString() method for the Person class we can also redefine the meaning of common operators for manipulating the class instances.

"This means that you can also override (most) operators for your own types.  That being said, please don’t go crazy with this. We’re giving you the keys to the car and trusting that you won’t turn around and drive it through the living room." - [dartlang.org]

| <  | +  | &#124; | [] |
|----|----|----|-----|
| >  | /  | ^  | []= |
| <= | ~/ | &  | ~  |
| >= | *  | << | == |
| -  | %  | >> |    |
* Truncating division operator: ~/

When using these operators they are actually calling a method.  For example, when using addition in the Dart language you can use the operator '+' to add the numbers 1 and 2, but under the hood of the language it is really a method call to the '+' operator, 1.+(2).

Looking at this example we can see that it will always be the left-hand argument that the operator will be looked up for.  This is a good thing to know when overloading these methods.

###The equality operator.
Probably the most popular operator to overload is going to be the equality operator.  The equality operator defines requirements for what is expected when this method is overwritten in your definition.  When comparing two Objects the default behavior of the equality operator is to return true if and only if the Object and the Object to compare with are the same object.  To override this method the following constraints are required.

* Total: It must return a boolean for all arguments. It should never throw or return null.
* Reflexive: For all objects o, o == o must be true.
* Symmetric: For all objects o1 and o2, o1 == o2 and o2 == o1 must either both be true, or both be false.
* Transitive: For all objects o1, o2, and o3, if o1 == o2 and o2 == o3 are true, then o1 == o3 must be true.

To overload the equality operator of the Person class above we can add the following definition to the Person class so that we can determine what will consider two Person objects to be equal.
```javascript
operator ==(Person p2) {
if ((firstName.compareTo(p2.firstName) == 0) &&
(lastName.compareTo(p2.lastName) == 0)) {
return true;
}
return false;
}
```

[Dart Homepage]:https://www.dartlang.org/
[dartlang.org]:https://www.dartlang.org/articles/idiomatic-dart/

---

#### SQL: `joins`
inner, outer, etc
jlewis

A "JOIN" in SQL is a keyword which tells the system to perform set like operations on two or more tables and returns a new set of rows and columns. This is one of the fundamental features of the database management system's "relational" capabilities. Each table can store data unique to itself and then "relate" this data to other tables containing shared data points. 

For example, if a Product table has related category information, a separate Category table is created with all possible categories and a unique identifier for each (the key column or columns). Then, the Product table is joined to the Categories table by the key to allow for the selection of category information not contained in the Products table. The Products table only needs to store the key for the category that it relates to, not all of the category information. The key column could simply be the name column, which would be its natural key, but many systems use a surrogate key, such as an integer and create an id column which uniquely identifies the record. Using the id key, tables can be related to each other by a single column rather than multiple columns, making the join much easier.

Multiple joins can be included in one statement, so any combination of tables is allowed, including joining a table to itself. A predicate, or boolean comparison, specifies which fields (columns) to match between the two tables. Multiple predicates can be specified in a single join using AND or OR. Other selection criteria are specified using the "WHERE" clause. In ANSI-standard SQL there are five types of joins: Inner Join, Left Outer Join, Right Outer Join, Full Outer Join and Cross Join.

The basic syntax for a join operation is something like this: 
```
SELECT [table_name].[column_name], [table_name].[column_name] AS alias, [table_name].*, ...
FROM left_table AS alias
JOIN (right_table, right_table2, ...)
ON (predicate AND/OR predicate)
WHERE predicate AND/OR predicate AND/OR IN (SELECT ...) AND/OR Other operators ...
ORDER BY [table_name].[column_name], ...
```
Standard comparison operators (=, <, <=, >, >=, != or <>) can be used in the predicate when comparing column values.

##### INNER JOIN or JOIN
The intersection of the two tables based on the join predicate that indicates which columns to compare. Only elements that match the join-predicate in both tables are included in the result set. This is the default behavior for a join.
```
SELECT Departments.department, Categories.category, Products.name, Products.description
FROM Departments
JOIN Categories ON Departments.department_id = Categories.department_id
JOIN Products ON Categories.category_id = Products.category_id AND/OR ... [Another predicate]
WHERE Departments.department_id = 10
```

##### OUTER JOINS
Outer joins are joins in which there does not need to be a matching predicate in both tables. There are three basic flavors.

**LEFT OUTER JOIN or LEFT JOIN**
The LEFT JOIN includes all records from the "left" table and only those that match the predicate in the "right" table. If there are no matching records in the LEFT table, then NULL is returned for the match. 

The following example selects all rows in the Departments (LEFT) table and only records in the Categories table that match the predicate.
```
SELECT *
FROM Departments
LEFT JOIN Categories ON Departments.department_id = Categories.department_id
WHERE Categories.id IS NULL --This gets only departments that have no related categories.
```

**RIGHT OUTER JOIN or RIGHT JOIN**
The RIGHT JOIN includes all records from the "right" table and only those that match the predicate in the "left" table. This is identical to the LEFT JOIN, except reversed.

The following example selects all rows in the Categories (RIGHT) table and only records in the Departments table that match the predicate.
```
SELECT *
FROM Departments
RIGHT JOIN Categories ON Categories.department_id = Departments.department_id --Order of tables in the predicate does not matter.
```

**FULL OUTER JOIN or FULL JOIN**
The union of the two tables based on the predicate. All elements from both tables are included in the result set, whether they match the predicate or not. This is effectively the same as combining the LEFT and RIGHT outer joins.
```
SELECT *
FROM Departments
FULL JOIN Categories ON Departments.department_id = Categories.department_id
```

##### CROSS JOIN (CARTESIAN PRODUCT)
Takes every element from a table and combines it with every element of another table. If the first table contains 4 rows and the second contains 10 rows, the result will be 40 rows. No predicate is specified in this type of join. A WHERE clause can be used to filter the results. Obviously, this is a dangerous query to run on large tables.
```
SELECT *
FROM Departments
CROSS JOIN Categories
```
This is the same as:
```
SELECT *
FROM Departments, Categories
```

##### Self Join
Joins are allowed between a table and itself. This feature can be used where a relation exists within the same table. An example of this might be a category table that has sub-categories. Instead of having two separate category tables, a single table can be used with each Category record specifying a "parent" category id in the same table.

Example:
[category_id], [name], [description], [parent_category_id]

```
SELECT Categories.*, SubCategories.* 
FROM Categories
JOIN Categories as SubCategories ON Categories.category_id = SubCategories.parent_category_id
```

##### Conclusion
SQL is a simple but powerful language for working with relational database systems. The basics are very easy to learn and very powerful. The syntax of the language is also very easy to understand. For any company that shares data between systems, an RDBMS will probably be used and SQL will be used for retrieving, updating, and storing data. It is essential to have experience with SQL!


---

#### SQL: `operators` &amp; `views`
adebaca

---

#### MicroPython: `controlling hardware`
jkniss


##### Basic Motor Control

 (See Bluetooth Control below)


##### Basic Accelerometer Control
 
 (next up...)


##### Light Sensor

```
from pyb import ADC
light = ADC(Pin('X7'))
light.read()
>>> 456
```


##### IR Sensor

```
from pyb import ADC
eyes = ADC(Pin('Y11'))
eyes.read()
>>> 2533
```


##### Bluetooth Control
[Demo Video](https://drive.google.com/file/d/0B9k3eDZYhuLoazZOaFN1bTJkZjQ/view?usp=sharing)

```
# main.py -- on pyboard
import pyb
from pyb import Pin
from pyb import UART
 
left_motor = Pin('X1', Pin.OUT_PP)
right_motor = Pin('X2', Pin.OUT_PP)
uart = UART(3,9600)
uart.init(9600, bits=8, stop=1, parity=None)
pyb.repl_uart(uart) //push repl to uart for control via bluetooth/phone
  
def lt():
    right_motor.low()
    left_motor.high()
    pyb.delay(200)

def rt():
    right_motor.high()
    left_motor.low()
    pyb.delay(200)

def stop():
    right_motor.low()
    left_motor.low()
    pyb.delay(200)

def go():
    right_motor.high()
    left_motor.high()
    pyb.delay(200)
```


Basic 

---

#### R: `graphical features`
charts
sbradbur
#Overview
R is an object-oriented, high-level, statistical programming language.  It is designed for statistical computing and graphics and is widely used by scientists and mathematicians.  R is dynamically and strongly typed and uses lexical scoping.  
#Graphical Features
R can be used to create many kinds of graphs.  R has built in functions for graphing, and the arguments of the function specify what data will be graphed.  This language makes it easy to visually represent datasets in a large variety of ways.   
A code example of making minimal graphs from built in data sets in R:
```
hist(faithful$eruptions)      
hist(faithful$waiting)
plot(faithful)			
boxplot(faithful$eruptions)	
stripchart(faithful$eruptions)	

plot(women)
lines(women)				#adding lines to a plot
pie(women$height)
```
You can make a lot of graphs with very little coding, but these graphs are pretty minimal.  R uses method overloading to allow you to change aspects of the graph.  The first argument specifies what will be graphed, and the rest set the values of built in variables.  
A code example, improving on an earlier graph: 
```
plot(faithful,
     main = "Old Faithful Eruptions",
     col = "red",
     col.main = "blue",
     col.lab = "purple",
     xlab = "Time between Eruptions (min)",
     ylab = "Duration of Eruption (min)")
```

---

#### C#: `typing system`

cowens

##### Typing
C# is strongly and statically typed. C# enforces type safety. These allow for increased stability in C# development. C# has a few interesting topics within typing, including *dynamics* and *vars*. 
##### Dynamics
C# has a unique type, *dynamic*. In essence, declaring an object of type dynamic allows for this object to bypass standard type checking. This allows for flexibility of use, but places the burden of type checking on the programmer to avoid any runtime errors that would normally have been caught at compile time. 
###### Example: 
```C#
using System;
using System.Drawing;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace Sandbox {
    class Program {
        static void Main(string[] args) {
            dynamic obj = "Hello World";
            foreach (char c in obj){
                Console.Write(c);
            }
            Console.WriteLine();
            obj = 1;
            obj = obj + 1;
            Console.WriteLine(obj);
            obj = 2.5;
            obj = obj * .75;
            Console.WriteLine(obj);
            obj = new Point(5, 10);
            Console.WriteLine(obj);
            Console.WriteLine("("+obj.X+","+obj.Y+")");
			obj.missingMethod();
            System.Threading.Thread.Sleep(10000);
        }
    }
}
```
In the above example, obj is used as a String, then an int, then a double, and finally a point. Each of these compile without error, and the program runs as you would expect, with obj adapting to each use as needed. This demonstrates the power of the dynamic type in C#. It isn't until the line `obj.missingMethod();` that we have a runtime error. The runtime is unable to bind the missingMethod() method, since it doesn't exist. This demonstrates the risk of using dynamics - it's up to the programmer to ensure type safety. The compiler will not catch issues like this. 
##### Vars
Another unique type for C# is *var*. Declaring an object of type var allows the compiler to determine what type the object should be implicitly. 
###### Example: 
```C#
using System;
using System.Drawing;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace Sandbox {
    class Program {
        static void Main(string[] args) {
            var obj = "Hello World";
            foreach (char c in obj){
                Console.Write(c);
            }
            Console.WriteLine();
            obj = 1;
            obj = obj + 1;
            Console.WriteLine(obj);
            obj = 2.5;
            obj = obj * .75;
            Console.WriteLine(obj);
            obj = new Point(5, 10);
            Console.WriteLine(obj);
            Console.WriteLine("("+obj.X+","+obj.Y+")");
			obj.missingMethod();
            System.Threading.Thread.Sleep(10000);
        }
    }
}
```
Unlike the above example for dyamics, declaring obj as a var works for the first use, but attempting to redefine obj as an int, double, or point results in compile errors - the compiler determined that obj should be a String and will treat it as a String for the rest of its use. 

---

#### C#: `debugging` &amp; `exception handling`
rlamichh

### Exceptions in C#

C# language's exception handling is similar to Java.

* Exceptions are object that inherits from System.Exception class
	- Constructors:

		Exception()

		Exception(String)

		Exception(SerializationInfo, Streaming context)

		Exception(String, Exception)

	- Properties:
	Stack trace, Source, Message, InnerException, HelpLink, etc

* Exceptions can be generated by the common language runtime (CLR), by third party libraries or by the application code using the throw keyword.

![alt tag](http://i.msdn.microsoft.com/dynimg/IC15013.png)

* It uses try, catch and finally keywords

	- When exception occurs in try block, the flow of control immediately jumps to an exception handler if it is present otherwise program terminates with error message.

	- If catch block defines exception variable, we can use it to get more information about the exception like printing the text description and stack trace of the exception.

	- If finally block is present the body will run whether there was exception or not.

Example:
```C#
static void Read_Write()
{
    System.IO.FileStream file = null;
    System.IO.FileInfo fileInfo = null;

    try
    {
        fileInfo = new System.IO.FileInfo("C:\\file.txt");

        file = fileInfo.OpenWrite();
        file.WriteByte(0xF);
    }
    catch(System.Exception e)
    {
        System.Console.WriteLine(e.Message);
    }
    finally
    {
        if (file != null)
        {
            file.Close();
        }
    }
}

// also can use specific type of exception in the catch
```

### Types of Exception

**User defined**

```C#
using System;

public�class InvalidInput: Exception
{
public InvalidInput(string message): base(message)
{}
}
```

ArgumentException: if the argument to a method is invalid

ArgumentNillException: if the argument is null

ArgumentOutOfRangeException: By substring method

ArrayTypeMismatchException: when an array element location is assigned to an object whose type is not compatible

DivideByZeroException

DirectoryNotFoundException

FileNotFoundException

IndexOutOfRangeException

InvalidCastException

IOException

NullReferenceException

OutOfMemory

StackOverFlowException

Etc..


### Demo in Visual Studio 2013

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

//using System.Diagnostics;

namespace DebuggingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Read_Write();
            //DebuggingWithBreakPoints();
            //ExceptionsDebugging();
            //Read_process();
        }

        static void Read_Write()
        {
            System.IO.FileStream file = null;
            System.IO.FileInfo fileInfo = null;

            try
            {
                fileInfo = new System.IO.FileInfo("C:\\file.txt");
                //fileInfo = new System.IO.FileInfo("A:\\TestFile.txt");

                file = fileInfo.OpenWrite();
                System.Console.WriteLine("The program was sucessful at reading the file");
                //file.WriteByte(0xF);
            }
            catch (System.Exception e)
            {
                System.Console.WriteLine(e.Message);
                System.Console.WriteLine(e.StackTrace);
            }
            finally
            {
                if (file != null)
                {
                    file.Close();
                }
            }
        }

        static void DebuggingWithBreakPoints()
        {
            int x = 5;
            int y = 7;

            int z = x + y;

            int a = x;

            System.Console.WriteLine(z);
        }

        static void ExceptionsDebugging()
        {
            // String abc = null;
            String abc = "hello everyone !!!";

            if (abc != null)
                System.Console.WriteLine(abc.Substring(0, 17));
        }

        static void Read_process()
        {
            System.Console.WriteLine("Please Input a number");
            int num = System.Console.Read();
            userExceptionCall(num);

            //try
            //{
            //    int num = System.Console.Read();
            //    userExceptionCall(num);
            //}
            //catch (Exception e)
            //{
            //    System.Console.WriteLine(e.Message);
            //}
        }

        static void userExceptionCall(int num)
        {
            if (num > 5)
                throw new UserException("This is User Exception. Enter something > 5");
        }
    }

    partial class UserException: Exception
    {
        public UserException(String message): base(message)
        {
        }
    }
}
```
---

#### C#: `anonymous types` &amp; `properties`
astout

---

#### C#: `OO` &amp; `classes`
dhampiki

Classes in C#
Daniel Hampikian

C#, like Java, is an object-oriented programming language.  This means that objects are the fundamental units of the language, where classes define an objects variables, methods, events, and properties, then the objects are created and called by classes and their defined properties are utilized by the calling class.  Object-oriented languages like C# support encapsulation, where a group of related properties and methods are treated as a single objet, inheritance, or the ability to create new classes based on an existing class, and polymorphism, or the ability to have multiple classes that can be used interchangeably.  Classes describe the type of object, like a blueprint, and the object is the building made from that blueprint.  

In C#, a class allows you to create custom types by grouping together variables, methods, and events, in a way similar to the class structure of Java.  A class functions like a roadmap that defines the data and behavior of a type.  A class can be declared as static, but if it is not it the client code calling the class can use it by creating objects or instances of that class which are assigned to a variable.  

Classes in C# support inheritance also like the Java language.  They are declared by using the class keyword. 
For example: 

```
public class ThisIsAClass
{
//The field:
public string aString; 

//A constructor that takes a string as an argument
public ThisIsAClass(string s) {
aString = s;
}
}
class Test
{
	static void Main()
{
	ThisIsAClass example = new ThisIsAClass(“Alright!”);
	Console.WriteLine(example.aString);

}
}
```
//output: Alright!

This class contains a field, a method, and a constructor.  

It is also interestingly possible to split the definition of a class over two or more source files.  
When this occurs different source files contain different section of the type of method definition and all parts are combined when the application is compiled.  When this occurs we have partial classes.  

This is pragmatic when large projects are worked on by multiple programers so that they can all work on the same class at the same time.  
When you are working on automatically generated source this is also pragmatic because code can be added to the class without having to recreate the source file.  Visual studio, for example, uses this approach when it creates Windows Forms.  
To split a class definition, you use the partial keyword modifier as shown:
```
public partial class Clowns
{
public void ClownWork()
{
}
}

public partial class Midgets 
{
public void MidgetWork()
{
}
}
```

The partial keyword indicates that other parts of the class can be defined in the namespace.  All parts must use the partial key word and be available to compile time to form the final type and must also have the same accessibility modifier, abstract, or sealed modifiers must be consistent across the whole class. 

The access modifiers of SC# are very similar to those of Java, where we have public, private, and protected modifier that limit access as follows:
public is not restricted, protected is limited tot he class or types derived from the containing class.  
And finally, private where access is strictly limited to the containing type. 
However, C# has a a internal, and protected internal type, where for internal access is limited to the current assembly and for protected internal access is limited to the current assembly or types derived from the containing class.  

References:

For classes my information comes mostly from:

http://msdn.microsoft.com/en-us/library/x9afc042.aspx

For partial classes my information comes mostly from:

http://msdn.microsoft.com/en-us/library/wa80x488.aspx


#### Python: `OO` &amp; `classes`
mhandysi

####Object Oriented Python
Python has been an __Object Oriented__ language since day one, making it extremely easy to use classes and objects in your programs.

#####Class Syntax

The syntax of a class in python is much like a method definition. You have the keyword __class__ followed by the class name followed by a colon. By convention th first letter of the class name is usually capitallized.

After the class declaration usually follows class variables, variable that are visible to every instance of the class object. Then the constructor and class methods.

Example Class: 
```python
class Cutlery(object):
	#class variables
	cutlery = 0
	#...
	#class constructor
	def __init__(self, utensil, type):
		self.utensil = utensil
		self.type = type
		#...
	#class methods
	def cutleryUse(self):
		#method body...
		print "Using %s %s" % (self.type, self.utensil)
		#...
	def cutleryWash(self):
		#method body...
		print "Washing %s %s" % (self.type, self.utensil)
		#...
	def cutleryDisplay(self):
		print "This is a %s %s" % (self.type, self.utensil)
```

Note: the __object__ keyword in the class definition will be discuessed when we get into inheritance. 

Note: the __init__ definition will be discussed as we get to private and public declarations.

#####Creating Objects
Creating object in python is simple enough; by using the class as a method. There is no __new__ keyword in python, we simply call our class and pass in our parameters.

Example Object:
```python
fork = Cutlery("Fork", "Salad")
spoon = Cutlery("Spoon", "Soup")
```
Note: the parameters in the object instantiation are one short according to our definition. But in python, the parameter self is much like __this__ in Java or C/C++ but it is not a definate keyword and acts as a scoping mechanism.

#####Accessing Objects
Accessing object properties in python is much like any other language. The methods are called from the object instantiation with the '.' operater.

Example Object Access:
```python
fork.cutleryUse()
fork.cutleryWash()
fork.cutleryDisplay()

spoon.cutleryUse()
spoon.cutleryWash()
spoon.cutleryDisplay()
```

Output:
```
Using Salad Fork
Washing Salad Fork
Salad Fork

Using Soup Spoon
Washing Soup Spoon
Soup Spoon
```
Note: When we called the methods defined in our class, we did not need to pass in the self parameter. Python does this automatically to access the local scope of our objects.

#####Class Inheritance
Now that we have the basic class figured out, what if we want to define specific utensils for the cutlery class and define what they are being used for. We can easily accomplish this via subclasses and inheritance.

In a note above I mentioned the __object__ parameter in the class definition. This is because most everything in python is based off of this __object__ class. In other words to make a subclass, we pass in the parent as a parameter to the definition.

Say we want to make classes the inherit from Cutlery and have a specified use. We do this by making a __Fork__, __Spoon__ and __Knife__ class and passing in the parent (__Cutlery__) as a parameter of sorts to the definition.

Example Subclasses:
```python
class Fork(Cutlery):
	#class variables for Fork objects
	
	def toss():
		print "Tossing Salad"

class Spoon(Cutlery):
	#class variables for Spoon objects

	def stir():
		print "Stirng Coffee"
	
class Knife(Cutlery):
	#class variables for Knife objects

	def cut():
		print "Cutting Steak"
	
```
Example SubObjects:
```python
saladFork = Fork("Fork", "Salad")
soupSpoon = Spoon("Spoon", "Soup")
steakKnife = Knife("Knife", "Steak")

saladFork.cutleryUse()
saladFork.toss()
soupSpoon.cutleryUse()
soupSpoon.stir()
steakKnife.cutleryUse()
steakKnife.cut()
```

Output:
```
Using Salad Fork
Tossing Salad
Using Soup Spoon
Stiring Coffee
Using Steak Knife
Cutting Steak
```
Note: there is no construtor in these subclasses. This is because they are inheriting everything from their parent class __Cutlery__. They are able to call parent methods as well as their own.

When creating objects from subclasses, if no constructor is defined, the parent constructor will take over. Which leads to Method Overriding in the next section.

#####Method Overriding:
In the example of inheritance, we made three subclasses. But we want to be able to tell each class a specific use for each utensil and a way to do that is to override the parent constructor. To do this we override the __init__ method from the parent.

Example Override:
```python
class Fork(Cutlery):
	def __init__(self, type, use):
		self.type = type
		self.use = use
	#...
class Spoon(Cutlery):
	def __init__(self, type, use):
		self.type = type
		self.use = use
	#...
class Knife(Cutlery):
	def __init__(self, type, use):
		self.type = type
		self.use = use
	#...
```

Note: each class overrides the __init__ method, but we have no way of telling the parent what it is. We need to call the parent constructor as well to define the utensil we are creating.

```python
class Fork(Cutlery):
	def __init__(self, type, use):
		Cutlery.__init__(self, "Fork", type)
		self.use = use
	#...

class Spoon(Cutlery):
	def __init__(self, type, use):
		Cutlery.__init__(self, "Spoon", type)
		self.use = use
	#...

class Knife(Cutlery):
	def __init__(self, type, use):
		Cutlery.__init__(self, "Knife", type)
		self.use = use
	#...
```
Now we have our personal constructors for each subclass. Each type of utensil has a pecific use, hence the __use__ variable which will remain only visible to each individual subclass.

Any method made inside a parent class can be overriden inside a subclass if it must have a different use from the parent.

#####Private & Public Data
It may have been noticed that the __init__ methods of our classes have two leading and trailing underscores. This is how python protects certain functions or variables.

Say we wanted to make it so no one knows how many utensils we actually have. We could do this by using two leading underscores.

Example Private variable:
```python
class Cutlery(object):
	
	__cutlery = 0

	def __init__(self, utensil, type):
		self.utensil = utensil
		self.type = type
		self.__cutlery += 1
		
	def getCutleryCount():
		print self.__cutlery	

cutlery = ("Fork", "Salad")
cutlery.getCutleryCount()
print cutlery.__cutlery
```

This code would run a error at the print statement because python sees the two underscores and internally changes th variable name to include the class name. _object.className__variable is what would be used for the print statement to work correctly.

```python
print cutlery._Cutlery__cutlery
```

### Python: `modules`
cbarton

---

#### Haskell: `monads`
jpack

---
