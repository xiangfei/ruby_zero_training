# Ruby 面向对象

---

## Ruby 类
<aside class="notes">
Ruby 是纯面向对象的语言，Ruby 中的一切都是以对象的形式出现。Ruby 中的每个值都是一个对象，即使是最原始的东西：字符串、数字，甚至连 true 和 false 都是对象。类本身也是一个对象，是 Class 类的一个实例。本章将向您讲解所有与 Ruby 面向对象相关的主要功能。
</aside>
- 类用于指定对象的形式，它结合了数据表示法和方法，把数据整理成一个整齐的包。类中的数据和方法被称为类的成员。
- 按照惯例，名称必须以大写字母开头，如果包含多个单词，每个单词首字母大写，但此间没有分隔符（例如：CamelCase）
---

## 定义 Ruby 对象
 - 类提供了对象的蓝图，所以基本上，对象是根据类进行创建的
 - new 关键字声明类的对象

```ruby
box1 = Box.new
box2 = Box.new

```

---

## initialize 方法
- initialize 方法是一个标准的 Ruby 类方法，与其他面向对象编程语言中的 constructor 工作原理类似

```ruby
class Box
   def initialize(w,h)
      @width, @height = w, h
   end
end

```

---

## 实例变量

- 实例变量是类属性，它们在使用类创建对象时就变成对象的属性
<aside class="notes">实例变量是类属性，它们在使用类创建对象时就变成对象的属性。每个对象的属性是单独赋值的，和其他对象之间不共享值。在类的内部，是使用 @ 运算符访问这些属性，在类的外部，则是使用称为访问器方法的公共方法进行访问。下面我们以上面定义的类 Box 为实例，把 @width 和 @height 作为类 Box 的实例变量。
  </aside>

---

## 访问器方法

- 为了在类的外部使用变量，我们必须在访问器方法内部定义这些变量，这些访问器方法也被称为获取器方法

```ruby
#!/usr/bin/ruby -w

# 定义类
class Box
   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end

   # 访问器方法
   def printWidth
      @width
   end

   def printHeight
      @height
   end
end

# 创建对象
box = Box.new(10, 20)

# 使用访问器方法
x = box.printWidth()
y = box.printHeight()

puts "Width of the box is : #{x}"
puts "Height of the box is : #{y}"


```


---

## 设置器方法

- 与用于访问变量值的访问器方法类似，Ruby 提供了一种在类的外部设置变量值的方式，也就是所谓的设置器方法


```ruby 
#!/usr/bin/ruby -w

# 定义类
class Box
   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end

   # 访问器方法
   def getWidth
      @width
   end
   def getHeight
      @height
   end

   # 设置器方法
   def setWidth=(value)
      @width = value
   end
   def setHeight=(value)
      @height = value
   end
end

# 创建对象
box = Box.new(10, 20)

# 使用设置器方法
box.setWidth = 30
box.setHeight = 50

# 使用访问器方法
x = box.getWidth()
y = box.getHeight()

puts "Width of the box is : #{x}"
puts "Height of the box is : #{y}"

```

---

## 实例方法

- 只能通过类实例来使用

```ruby
#!/usr/bin/ruby -w

# 定义类
class Box
   # constructor method
   def initialize(w,h)
      @width, @height = w, h
   end
   # 实例方法
   def getArea
      @width * @height
   end
end

# 创建对象
box = Box.new(10, 20)

# 调用实例方法
a = box.getArea()
puts "Area of the box is : #{a}"

```

---

## 类方法

- 类方法使用 def self.methodname() 定义，类方法以 end 分隔符结尾

```ruby
#!/usr/bin/ruby -w

class Box

   def self.printCount()
      puts "Box count is  10"
   end
end


# 调用类方法来输出盒子计数
Box.printCount()
```

---

## 类变量

- 类变量是在类的所有实例中共享的变量。换句话说，类变量的实例可以被所有的对象实例访问。类变量以两个 @ 字符（@@）作为前缀

```ruby
#!/usr/bin/ruby -w

class Box
   # 初始化类变量
   @@count = 0
   def initialize
      # 给类变量赋
      @@count += 1
   end
end

# 创建两个对象
box1 = Box.new
box2 = Box.new
puts Box.class_variable_get "@@count" 


```

---

## to_s 方法

- 任何类都有一个 to_s 实例方法来返回对象的字符串表示形式


```ruby
#!/usr/bin/ruby -w

class Box
   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end
   # 定义 to_s 方法
   def to_s
      "(w:#@width,h:#@height)"  # 对象的字符串格式
   end
end

# 创建对象
box = Box.new(10, 20)

# 自动调用 to_s 方法
puts "String representation of box is : #{box}"
```

---

## 访问控制
- Ruby提供了三个级别的保护实例方法的级别
 - **public**
 - **private**
 - **protected**

--- 

## Public Methods

 - 任何类都可以访问。方法默认为公用初始化

```ruby
class Box

  def area
    puts "area"
  end
end
class Box1 < Box

end
Box.new.area
Box1.new.area
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
area
area
    </code>
  </pre>
</div>


---
## Private Methods
 - 不能被访问，或者甚至从类的外部浏览。只有类方法可以访问私有成员。

```ruby
class Box
  def ss
    wide
  end
  private 
  def wide
    puts "wide" 
  end
end
Box.new.ss
Box.new.wide
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
wide
2.4.2 :023 > Box.new.wide
NoMethodError: private method `wide' called for #<Box:0x0000000006d376c8>
  from (irb):23
    </code>
  </pre>
</div>

---
## Protected Methods
 - 受保护的方法可以被调用，只能通过定义类及其子类的对象。访问保存在类内部

```ruby
class Box

  protected
  def height
    puts "height"
  end

end

Box.new.height
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
NoMethodError: protected method `height' called for #<Box:0x0000000006c5b718>
  from (irb):48
    </code>
  </pre>
</div>

---


## class 继承

<aside class="notes">
  <p style="text-indent:2em">在面向对象的编程中最重要的概念之一是继承。继承允许我们定义一个类在另一个类的项目，这使得它更容易创建和维护应用程序。</p>
  <p style="text-indent:2em">继承也提供了一个机会，重用代码的功能和快速的实现时间，但不幸的是Ruby不支持多级的继承，但Ruby支持混入。一个mixin继承多重继承，只有接口部分像一个专门的实现。</p>
  <p style="text-indent:2em">当创建一个类，而不是写入新的数据成员和成员函数，程序员可以指定新的类继承现有类的成员。这种现有的类称为基类或父类和新类称为派生类或子类。</p>
  <p style="text-indent:2em">Ruby也支持继承。继承和下面的例子解释了这个概念。扩展类的语法很简单。只需添加一个<字符的超类声明的名称。</p>
</aside>

```ruby
class A
  def s
    puts 12
  end
end
# 
class B < A 

end
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :032 > b=B.new
 => #<B:0x000000000103d620> 
2.4.2 :033 > b.s
12
 => nil 

    </code>
  </pre>
</div>

---
##  class 方法重载


<aside  class="notes">
  
  <p style="text-indent:2em">虽然可以在派生类中添加新的函数，但有时想改变的行为已经在父类中定义的方法。只
需通过保持相同的方法名和重写该方法的功能</p>
</aside>


```ruby
class A
  def s
    puts 12
  end
end

class B < A 
  def s
    puts 13
  end
end

```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :032 > b=B.new
 => #<B:0x000000000103d620> 
2.4.2 :033 > b.s
13
 => nil 

    </code>
  </pre>
</div>

---

## 运算符重载

<aside class="notes">
  我们希望使用 + 运算符执行两个 Box 对象的向量加法，使用 * 运算符来把 Box 的 width 和 height 相乘，使用一元运算符 - 对 Box 的 width 和 height 求反。下面是一个带有数学运算符定义的 Box 类版本：

</aside>


```ruby
class Box
  def initialize(w,h) # 初始化 width 和 height
    @width,@height = w, h
  end

  def +(other)         # 定义 + 来执行向量加法
    Box.new(@width + other.width, @height + other.height)
  end

  def -@               # 定义一元运算符 - 来对 width 和 height 求反
    Box.new(-@width, -@height)
  end

  def *(scalar)        # 执行标量乘法
    Box.new(@width*scalar, @height*scalar)
  end
end

```

---

## 冻结对象

<aside class="notes">
  有时候，我们想要防止对象被改变。在 Object 中，freeze 方法可实现这点，它能有效地把一个对象变成一个常量。任何对象都可以通过调用 Object.freeze 进行冻结。冻结对象不能被修改，也就是说，您不能改变它的实例变量。

您可以使用 Object.frozen? 方法检查一个给定的对象是否已经被冻结。如果对象已被冻结，该方法将返回 true，否则返回一个 false 值。下面的实例解释了这个概念

</aside>

```ruby
#!/usr/bin/ruby -w

# 定义类
class Box
   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end

   # 访问器方法
   def getWidth
      @width
   end
   def getHeight
      @height
   end

   # 设置器方法
   def setWidth=(value)
      @width = value
   end
   def setHeight=(value)
      @height = value
   end
end

# 创建对象
box = Box.new(10, 20)

# 让我们冻结该对象
box.freeze
if( box.frozen? )
   puts "Box object is frozen object"
else
   puts "Box object is normal object"
end

# 现在尝试使用设置器方法
box.setWidth = 30
box.setHeight = 50

# 使用访问器方法
x = box.getWidth()
y = box.getHeight()

puts "Width of the box is : #{x}"
puts "Height of the box is : #{y}"
```

---

## 类常量

- 使用大写

<aside class="notes">
  您可以在类的内部定义一个常量，通过把一个直接的数值或字符串值赋给一个变量来定义的，常量的定义不需要使用 @ 或 @@。按照惯例，常量的名称使用大写。

一旦常量被定义，您就不能改变它的值，您可以在类的内部直接访问常量，就像是访问变量一样，但是如果您想要在类的外部访问常量，那么您必须使用 classname::constant，如下面实例所示

</aside>


```ruby
#!/usr/bin/ruby -w

# 定义类
class Box
   BOX_COMPANY = "TATA Inc"
   BOXWEIGHT = 10
   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end
   # 实例方法
   def getArea
      @width * @height
   end
end

# 创建对象
box = Box.new(10, 20)

# 调用实例方法
a = box.getArea()
puts "Area of the box is : #{a}"
puts Box::BOX_COMPANY
puts "Box weight is: #{Box::BOXWEIGHT}"
```

---

## 使用 allocate 创建对象

- 跳过initialize 构造器

<aside class="notes">
  
可能有一种情况，您想要在不调用对象构造器 initialize 的情况下创建对象，即，使用 new 方法创建对象，在这种情况下，您可以调用 allocate 来创建一个未初始化的对象，如下面实例所示：

</aside>

```ruby
#!/usr/bin/ruby -w

# 定义类
class Box
   attr_accessor :width, :height

   # 构造器方法
   def initialize(w,h)
      @width, @height = w, h
   end

   # 实例方法
   def getArea
      @width * @height
   end
end

# 使用 new 创建对象
box1 = Box.new(10, 20)

# 使用 allocate 创建两一个对象
box2 = Box.allocate

# 使用 box1 调用实例方法
a = box1.getArea()
puts "Area of the box is : #{a}"

# 使用 box2 调用实例方法
a = box2.getArea()
puts "Area of the box is : #{a}"
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Area of the box is : 200
test.rb:14: warning: instance variable @width not initialized
test.rb:14: warning: instance variable @height not initialized
test.rb:14:in `getArea': undefined method `*' 
   for nil:NilClass (NoMethodError) from test.rb:29
    </code>
  </pre>

</div>

---
## Class

```ruby
class Person
  def initialize(name)
    @name = name
  end
end

puts Person.new('Xi Qi') # => #<Person:0x007fc623086218>

```

---

### Open Classes/Monkeypatch

> In Ruby, classes are never closed

```ruby
class Person
  def to_s
    "Person #{@name}"
  end
end

puts Person.new("Xi Qi") # => Person Xi Qi
```

---

### Inside Class Definitions

- the class keyword in Ruby is more like a scope operator than a class declaration
- it does create classes that don’t yet exist, but you might argue that it does this as a side effect
- For **class**, the core job is to move you in the context of the class, where you can define methods

```ruby
class Person
  puts "#{self}-#{self.class}-#{self.name}" # => Person-Class-Person
end
```

---

### Inheritance

```ruby
class Programmer < Person
  def code
    "puts 'Hello, World'"
  end
end

p Programmer.superclass # => Person
p Person.superclass # => Object
p Object.superclass # => BasicObject
p BasicObject.superclass # => nil
```
---

## Object

an object simply contains

- its instance variables and
- a reference to its class

---

### Instance Variables

```ruby
class Programmer
  def sleep
    @eyes = 'closed'
  end
end

programmer = Programmer.new('Xi Qi')
p programmer.instance_variables # => [:@name]

programmer.sleep
p programmer.instance_variables # => [:@name, :@eyes]
```

---

## Module

### module methods

```ruby
module MyModule
  def self.meth
    "module methods"
  end
end

p MyModule.meth # => "module methods"
```

---

### Namespaces

```ruby
module MyModule
  MyConstant = 'Outer constant'

  class MyClass
    MyConstant = 'Inner constant'
  end
end

p MyModule::MyConstant # => "Outer constant"
p MyModule::MyClass::MyConstant # => "Inner constant"
p MyModule::MyClass.new # => #<MyModule::MyClass:0x007f881a0a34b8>
```

---

### Mixins

```ruby
module Debug
  def who_am_i?
    "#{self.class.name} (id: #{self.object_id}): #{self.name}"
  end
end

class Phonograph
  include Debug
  attr_reader :name
    def initialize(name)
      @name = name
    end
end

ph = Phonograph.new("West End Blues")
p ph.who_am_i? # => "Phonograph (id: 70166168000260): West End Blues"
```

---

## Practice Time

- Module
- Open Classes

```ruby
p [1,2,3,4,5].sum # =>15
p ('a'..'m').sum # => "abcdefghijklm"
```

---

```ruby
module Summable
  def sum
    inject(:+)
  end
end

class Array
  include Summable
end

class Range
  include Summable
end
```

---

### module Enumerable

```ruby
class Colors
  include Enumerable

  def each
    yield "red"
    yield "green"
    yield "blue"
  end
end

colors = Colors.new
p colors.map(&:reverse) # => ["der", "neerg", "eulb"]
```

---

## Practice Time

- mixin Enumerable
- String#scan

```ruby
finder = VowelFinder.new("the quick brown fox jumped")
p finder.inject(:+) # => "euiooue"
```

---

## Story of `puts`

```ruby
puts "Hello, World"
```

---

### an Object named main

```ruby
puts self # => main
puts self.class # => Object
```

---

### Method Lookup

```ruby
class Programmer < Person
  def code
    "puts 'Hello, World'"
  end
end

xqi = Programmer.new('Xi Qi')
p Programmer.new('Xi Qi').code # => "puts 'Hello, World'"
p xqi.class # => Programmer
```

---

#### a class is an object

```ruby
p "hello".class # => String
p String.class # => Class
p Class.class # => Class
```

```ruby
p Object.superclass # => BasicObject
p BasicObject.superclass # => nil
```

```ruby
p Class.superclass # => Module
p Module.superclass # => Object
```

---
![Object model diagram](https://raw.githubusercontent.com/jiukunz/tw-ruby-training/master/img/object-model-diagram.png)
---

#### `??#puts`

Ruby looks up the method by following the rule

> one step to the right, then up

```ruby
p Object.method(:puts) # => #<Method: Class(Kernel)#puts>
```

---

#### ancestors

```ruby
p Object.ancestors # => [Object, Kernel, BasicObject]

p Kernel.class # => Module
```

---

```ruby
module Debug
  def who_am_i?
    "#{self.class.name} (id: #{self.object_id}): #{self.name}"
  end
end

class Phonograph
  include Debug
  attr_reader :name
    def initialize(name)
      @name = name
    end
end

p Phonograph.ancestors # => [Phonograph, Debug, Object, Kernel, BasicObject]
```

---

#### include classes / proxy classes

When you include a module in a class (or even in another module), Ruby plays a little trick. 

It creates an anonymous class that wraps the module and inserts the anonymous class in the chain, just above the including class itself

---

![Method lookup with modules](https://raw.githubusercontent.com/jiukunz/tw-ruby-training/master/img/method-lookup-with-modules.png)


---

#### Practice Time

`??#new`

---

```ruby
p Object.class.ancestors
# => [Class, Module, Object, Kernel, BasicObject]

p Class.instance_methods(false) # => [:allocate, :new, :superclass]
```

---

### Method Execution

#### receiver

The receiver is simply the object that you call a method on. For example, if you write 

```ruby
my_string.reverse()
```

then `my_string` is the receiver

---

#### self

- Every line of Ruby code is executed inside **current object**
- The current object is also known as self
- when you call a method, the receiver becomes self
- From that moment on, all instance variables are instance variables of self, and
- all methods called without an explicit receiver are called on self

```ruby
class MyClass
  def testing_self
    p self # => #<MyClass:0x007f884b8a35d8>
    @var = 10
    my_method
    self
  end

  def my_method
    @var = @var + 1
  end
end

p self # => main
obj = MyClass.new
p obj # => #<MyClass:0x007f884b8a35d8>
p obj.testing_self # => #<MyClass:0x007f884b8a35d8 @var=11>
```

---

### What private Really Means

```ruby
self.puts 'Hello, World'
# => NoMethodError: private method `puts' called for main:Object
```

private methods come from two rules working together: 

1. you need an explicit receiver to call a method on an object that is not yourself
2. private methods can be called only with an implicit receiver

---

```ruby
class A
  private
  def a_private_method
    puts "a private method"
  end
end


class B < A
  def a_public_method
    a_private_method
  end
end

B.new.a_public_method # => a private method
```

---

## Homework


```ruby
p1 = Person.new("Matz")
p2 = Person.new("Guido")
p3 = Person.new("Larry")
puts [p1, p2, p3].sort # => Guido\nLarry\nMatz
```

---

## References

- http://rubylearning.com/satishtalim/ruby_open_classes.html
- https://en.wikipedia.org/wiki/Object-oriented_programming
- [Metaprogramming Ruby](http://book.douban.com/subject/4086938/)
- [Programming Ruby 1.9 & 2.0 (4th edition): The Pragmatic Programmers' Guide](http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0)
