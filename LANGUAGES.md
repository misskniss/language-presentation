

#### Ruby: `mixins`
acole
TEST
--

#### Ruby: `classes` `inheritance`
kgrosh
I'm Adding Stuff Here!
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

module Identifier
   statement1
   statement2
   ...........
end


And here is a simple example of module:


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


If a third program wants to use these modules, it can simply load the two files using the Ruby require statement, and reference the qualified names. 
The Ruby require statement is similar to the import statement of Java and the include statement of C and C++. It does not matter using require “area.rb” or require “area.”

require “area.rb”
require “shape”

x = Area.round(1)
fact = Shape.round(Shape::YES)

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

---

#### Scala: `pattern matching` 
btombari

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

#### Dart: `libraries &amp; visibility`
tfogdall

Adding the line described in part.0.

---

#### Dart: `classes` &amp; `operator overloading`
cjohnson

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

---

#### C#: `typing system`
dynamics, vars 
cowens

---

#### C#: `debugging` &amp; `exception handling`
rlamichh

---

#### C#: `anonymous types` &amp; `properties`
astout

---

#### C#: `OO` &amp; `classes`
dhampiki

---

#### Python: `OO` &amp; `classes`
mhandysi

---

#### Python: `modules`
cbarton

---

#### Haskell: `monads`
jpack

---
