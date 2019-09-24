# Ruby 元编程



---

# 元编程
> *什么是元编程*

- 元编程是编写代码的代码.

---

## 类定义解密

<aside class="notes">
  下面的例子定义了class D, 第一次定义class不存在，定义了class D，并定义a方法
  第二次 class D 已经存在了，直接打开类定义了 b方法
  在ruby class不会关闭

</aside>

- ruby的class更像一个作用域字符，可以创建不存在的类
- 带到类的上下文中，可以定义其中的方法


```ruby

class D
  def a
  end
end

class D
  def b
  end
end

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :106 > D.new.a
 => nil 
2.4.2 :107 > D.new.b
 => nil 

    </code>
  </pre>

</div>

---

## 类与模块

- 每个类都是一个模块，类就是带有三个方法（new，allocate，superclass）的增强模块，通过这三个方法可以组织类的继承结构，并创建对象
- Ruby中的类和模块的概念十分接近，完全可以将二者相互替代，之所以同时保留二者的原因是为了保持代码的清晰性
- 模块机制可以用来实现类似其它语言中的命名空间(Namespace)概念

---

## 什么是对象

- 对象就是一组实例变量外加一个指向其类的引用。对象的方法并不存在于对象本身，而是存在于对象的类中。

---

## 什么是类

- 类就是一个对象(Class类的一个实例)外加一组实例方法和一个对其超类的引用。Class类是Module类的子类，因此一个类也是一个模块。

```ruby
# 动态定义类
String.class #Class
Class.class # Class

Book = Class.new do
    def foo
        "foo!"
    end
 
    #Both method declaration types work
 
    define_method('title') do
        "All My Friends Are Dead"
    end
end
```



---

## load与require方法的异同

- 通过load和require都可以进行导入别人的代码，不同的是load方法用来加载代码，如果不希望污染当前的命名空间，需要通过load(‘file.rb’,true)显式的要求创建一个匿名模块来，接管file.rb的常量，require用于导入类库，此外，就加载次数上load方法每次调用都会再次运行所加载文件，require则对每个库文件只加载一次


---

## prepend、include与祖先链

- 祖先链用于描述Ruby对象的继承关系，因为类与模块是父子关系，所以祖先链中也可以包含模块，prepend与include分别可以向链中添加模块，不同的是调用include方法，模块会被插入祖先链，当前类的正上方，而prepend同样是插入到祖先链，但位置其他却在当前类的正下方,另外通过Class.ancestors可以查看当前的祖先链



---

## private规则

- 不能通过明确指定接受者来调用私有方法。私有方法只能通过隐性的接受者self调用（Object#send是个例外）


---

## self相关

- 调用一个方法时，接受者会扮演self角色 任何没有明确指定接受者的方法调用，都当做是调用self的方法 定义一个模块(或类)时，该模块(或类)会扮演self角色



---

## 打开类

- ruby的class更像是一个作用于操作符而不是类定义语句，它可以创建一个不存在的类，也可以打开一个已定义的类，然后向内添加新的方法和属性，这种技术称为"打开类"技术。

```ruby
class String

  def to_alphanumber

    self.gsub /^\w\s/, ''

  end
end
```

---

## 猴子补丁

- 如果你粗心地为某个类添加了新功能，同时覆盖了类原来的功能，进而影响到其他部分的代码，这样的patch称之为猴子补丁(Monkeypatch)

```ruby
class String

  def to_alphanumber

    return 123

  end
end

```


---

## 动态定义方法

- 减少重复的代码

```ruby

[:foo ,:baz , :bar].each do |s|
    define_method(s) do
        puts "#{s} was called"
    end
end

class MyClass
    define_method :my_method do |my_arg|
        my_arg * 3
    do
end

obj = MyClass.new
obj.my_method(2)

```

---

## 调用动态方法


```ruby
[:foo ,:baz , :bar].each do |s|

  send s
end

```

---

## 魔法方法

<aside class="notes">
  
我们将会得到一个 无此方法的错误，因为 Book 实例不知道如果处理 read 这个方法。但是它也并不是不能处理。让我们来引入 method_missing 方法。

</aside>

```ruby
class Book
end
 
b = Book.new
b.read # => return no method error


class Book
    def method_missing(method, *args, &block)
        puts "You called: #{method}(#{args.join(', ')})"
        puts "(You also passed it a block)" if block_given?
    end
end

```

---

## 动态代理


- 对一些封装过的对象，通过method_missing方法收集调用，并把这些调用转发到被封装的对象，这一过程称为动态代理,其中method_missing体现了动态，转发体现了代理

---

## const_missing


- 与method_missing类似，还有关于常量的const_missing方法，当引用一个不存在的常量时，Ruby会把这个常量名作为一个符号传递给const_missing方法。

---

## 白板类(blank slates)

- 拥有极少方法的类称为白板类，通过继承BasicObject类，可以迅速的得到一个白板类。除了这种方法以外，还可以通过删除方法来将一个普通类变为白板类。


---

## 删除方法

- undef_method , remove_method

- 二者的区别是Module#undef_method会删除所有(包括继承而来的)方法。而Module#remove_method只删除接受者自己的方法，而保留继承来的方法。


---

## 代码块作用域


- Ruby中不具备嵌套作用域(即在内部作用域，可以看到外部作用域的)的特点，它的作用域是截然分开的，一旦进入一个新的作用域，原先的绑定会被替换为一组新的绑定。

程序会在三个地方关闭前一个作用域，同时打开一个新的作用域，它们是:

 - 类定义class
 - 模块定义 module
 - 方法定义 def


---


## 扁平化作用域


- 从一个作用域进入另一个作用域的时候，局部变量会立即失效，为了让局部变量持续有效，可以通过规避关键字的方式



```ruby
my_var = "Success"
class MyClass
    puts my_var  #这里无法正确打印"Success"
    def my_method
        puts my_var  #这里无法正确打印"Success"
    end
end


my_var = "Success"
MyClass = Class.new do
    puts "#{my_var} in  the class definition"
    define_method :my_method do
        "#{my_var} in the method"
    end
end

```

---

## 共享作用域

-   将一组方法定义到，某个变量的扁平作用域中，可以保证变量仅被有限的几个方法所共享。这种方式称为共享作用域

<aside class="notes">

  这个BasicObject#instance_eval有点类似JS中的bind方法，不同的时，bind是将this传入到对象中，而instance_eval则是将代码块(上下文探针Context Probe)传入到指定的对象中，一个是传对象，一个是传执行体。通过这种方式就可以在instance_eval中的代码块里访问到调用者对象中的变量
因为调用instance_eval后，将调用者作为了当前的self，所以作用域更换到了class C中，之前的作用域就不生效了。这时如果还想访问到之前@y变量，就需要通过参数打包上@y一起随instance_eval转义，但因为instance_eval不能携带参数，所以使用其同胞兄弟instance_exec方法。

此外，instance_eval方法还有一个双胞胎兄弟：instance_exec方法。相比前者后者更加灵活，允许对代码块传入参数。

因为调用instance_eval后，将调用者作为了当前的self，所以作用域更换到了class C中，之前的作用域就不生效了。这时如果还想访问到之前@y变量，就需要通过参数打包上@y一起随instance_eval转义，但因为instance_eval不能携带参数，所以使用其同胞兄弟instance_exec方法。



</aside>


```ruby
class MyClass
    def initialize
        @v = 1
    end
end
obj = MyClass.new

obj.instance_eval do
    self    #=> #<MyClass:0x33333 @v=1>
    @v      #=> 1  
end

v = 2
obj.instance_eval { @v = v }
obj.instance_eval { @v }   # => 2


class C
    def initialize
        @x = 1
    end
end
class D
    def twisted_method
        @y = 2
        #C.new.instance_eval { "@x: #{@x}, @y>: #{y}" }
        C.new.instance_exec(@y) { |y| "@x: #{@x}, @y: #{y}" }
    end
end
#D.new.twisted_method   # => "@x: 1, @y: "
D.new.twisted_method   # => "@x: 1, @y: 2"

```

---


## 洁净室

- 一个只为在其中执行块的对象，称为洁净室，其只是一个用来执行块的环境。可以使用BasicObject作为洁净室是个不错的选择，因为它是白板类，内部的变量和方法都比较有限，不会引起冲突。


---

## Proc对象


<aside class="notes">
  除了上面的四种之外，还有一种通过&操作符的方式，将代码块与Proc对象进行转换。如果需要将某个代码块作为参数传递给方法，需要通过为这个参数添加&符号，并且其位置必须是在参数的最后一个

&符号的含义是： 这是一个Proc对象，我想把它当成代码块来使用。去掉&符号，将能再次得到一个Proc对象。
</aside>

- Proc是由块转换来的对象



```ruby
inc = Proc.new { | x | x + 1}
inc.call(2)  #=> 3

# 法二
inc = lambda {| x | x + 1 }
inc.call(2)  #=> 3

# 法三
inc = ->(x) { x + 1}
inc.call(2) #=> 3

# 法四
inc = proc {|x| x + 1 }
inc.call(2) #=> 3

def my_method(&the_proc)
    the_proc
end

p = my_method {|name| "Hello, #{name} !"}
p.class   #=> Proc
p.call("Bill")   #=> "Hello,Bill"


def my_method(greeting)
    "#{greeting}, #{yield}!"
end

my_proc = proc { "Bill" }
my_method("Hello", &my_proc)
```

---

## Proc与Lambda对比

- Proc、Lambda的return含义不同; lambda中的return表示的仅仅是从lambda中返回。而proc中，return的行为则不同，其并不是从proc中返回，而是从定义proc的作用域中返回。即相当与在你的业务代码处返回

<aside class="notes">
  使用Lambda方法创建的Proc与其它方式创建的Proc是有一些差别的，用lambda方法创建的Proc称为lambda,而用其他方式创建的则称为proc。通过Proc#lambda?可以检测Proc是不是lambda。

</aside>


```ruby

def double(callable_object)
    p = Proc.new { return 10 }
    result = p.call   
    return result * 2 # 不可达的代码
end

doubl
```

---
## Proc与Lambda之间的选择

- lambda更直观，更像是一个方法，参数要求更加严格，return也更像是方法定义中的return，往往Ruby程序员会将lambda作为第一选择

---


## 可调用对象

- 代码块(不是真正的对象，但是它们是"可调用的") 在定义它们的作用域中执行
- proc: Proc类的对象与代码块一样，也在定义自身的作用域中执行
- lambda: 同样是Proc类的对象，但跟普通的proc有细微差别。与代码块与proc一样都是闭包，也在定义自身的作用域中执行
- 方法: 绑定于一个对象，在 所绑定对象的作用域中执行。他们也可以与这个作用域解除绑定，然后再重新绑定到另一个对象的作用域中


---

## Method 对象

- 通过Kernel#method方法，可以获得一个用Method对象表示的方法，在之后可以用Method#call方法对其进行调用。同样也可以用Kernel#singleton_method方法把单件方法名转换为Method对象


```ruby
class MyClass
    def initialize(value)
        @x = value
    end
    def my_method
        @x
    end
end

obj = MyClass.new(1)
m = obj.method :my_method
m.call   #=> 1


```

---

## 自由方法

- 与普通方法类似，不同的是它会从最初定义它的类或模块中脱离出来(即脱离之前的作用域)，通过Method#unbind方法，可以将一个方法变为自由方法。同时，你也可以通过调用Module#instance_method获得一个自由方法


<aside class="notes">
  
  上面代码中的UnboundMethod对象，不能够直接用来调用，不过可以将一个UnboundMethod方法绑定到一个对象上，使其再次成为一个Method对象，然后再被调用执行。

上面的绑定过程可以通过UnboundMethod#bind方法把UnboundMethod对象绑定到一个对象上，从某个类中分离出来的UnboundMethod对象只能绑定在该类及其子类对象上，不过从模块中分离出来的UnboundMethod对象在Ruby2.0后就不在有此限制了。

此外还可以将UnboundMethod对象传递给Module#define_method方法
</aside>

```ruby
module MyClass
    def my_method
        42
    end
end

unbound = MyModule.instance_method(:my_method)
unbound.class  #=> UnboundMethod


```

---

## 类的返回值
 
- 像方法一样，类定义也会返回最后一条语句的值:

```ruby
result = class MyClass
    self
end
result #=> MyClass

```

---

## 当前类

<aside class="notes">
  
  Ruby中并没有类似当前对象self一样的明确引用，不过在追踪当前类的时候，可以遵循下面几条:

在程序顶层，当前类是Object，这是main对象所属的类。
在一个方法中，当前类就是当前对象的类。(在一个方法中用def关键字定义另一个方法，新定义的方法会定义在self所属的类中。因为Ruby解释器总是追踪当前类(或模块)的引用，所以使用def定义的方法都成为当前类的实例方法了)

当用class关键字打开一个类时(或module关键字打开模块)，那个类称为当前类

</aside>

- 与当前对象self一样，同时还存在当前类（或模块）
 - 在程序顶层，当前类是Object，这是main对象所属的类
 - 在一个方法中，当前类就是当前对象的类


```ruby

class C
    def m1
        def m2; end
    end
end

class D < C; end

obj = D.new
obj.m1

C.instance_methods(false)   #=> [:m1, :m2]


```

---


## class_eval方法

- 会在一个已存在的类的上下文中执行一个块。使用该方法可以在不需要class关键字的前提下，打开类
- class_eval与Object#instance_eval方法相比，后者instance_eval方法只能修改self，而class_eval方法可以同时修改self与当前类。
- 此外class_eval的另一个优势就是可以利用扁平作用域，规避class关键字的作用域门问题。

---

## instance_eval 与 class_eval的选择

- 通常使用instance_eval方法打开非类的对象
- 而用class_eval方法打开类定义，然后用def定义方法

---

## 单件方法

- Ruby允许给单个对象增加方法,这种只针对单个对象生效的方法，称为单件方法

<aside class="notes">
  
  另外，除了上面使用的定义方法，还可以通过Object#define_singleton_method方法来定义单件方法


</aside>

```ruby
str = "just a regular string"

def str.title?
    self.upcase == self
end

str.title?  # => false
str.methods.grep(/title?/) # => [:title?]
str.singleton_methods   #=> [:title?]

str.class # => String
String.title?  #=>  NoMethodError
```

---

## 单件方法与类方法

- 类方法的实质是: 它是一个类的单件方法

<aside class="notes">
  


</aside>

```ruby
def obj.a_singleton_method

end

def MyClass.another_class_method

end
```

---


## 类宏 attr_accessor

- attr_accessor , attr_reader , attr_writer
<aside class="notes">
  Ruby对象没有属性，如果希望得到一些像属性的东西，需要分别定义一个读方法和写方法（也就是java、objc中的set和get方法)，最直接的可以这样:

</aside>

```ruby
class MyClass
    def my_attribute=(value)
        @my_attribute =value    
    end
    def my_attribute
        @my_attribute
    end
end

obj = MyClass.new
obj.my_attribute = 'x'
obj.my_attribute    #=> 'x'

class MyClass
  attr_accessor :my_attribue 
end

```

---

## 单件类

<aside class="notes">
  
首先,单件方法不会在obj中，因为obj不是一个类，其次它也不在MyClass中，那样的话所有的MyClass都应该能共享调用这个方法，也就构不成单件类了。同理，单件方法也不能在祖先链的某个位置(类似superclass: Object)中。正确的位置是在单件类中，这个类其实就是我们在irb中向对象询问它的类时(obj.class)得到的那个类，不同的是这类与普通的类还是有稍稍不同的。也可以称其为元类或本征类。

</aside>

- Ruby中对象的方法的查找顺序是: 先向右，再向上，其含义就是先向右找到对象的类，先在类的实例方法中尝试查找，如果没有找到，再继续顺着祖先链找

---

## 打开单件类

- Object#singleton_class
- 通过传统的关键词class配合特殊的语法


```ruby 

class << an_object
    # 自己的代码
end

obj = Object.new
singleton_class = class << obj
    self
end
singleton_class.class  # => Class

"abc".singleton_class


```

---


## 单件类的特性

- 每个单件类只有一个实例（被称为单件类的原因），而且不能被继承
- 单件类是一个对象的单件方法的存活所在


---

## 引入单件类后的方法查找

- 先从对象的单件类中开始查找
- 没找到普通类开始查找

<aside class="notes">
  
基于上面对单件类的基本认识，引入单件类后，Ruby的方法查找方式就不应该是先从其类(普通类)开始，而是应该先从对象的单件类中开始查找，如果在单件类中没有找到想要的方法，它才会开始沿着类(普通类)开始，再到祖先链上去找。这样从单件类之后开始，一切又回到了我们在没有引入单件类时候的次序。



</aside>


```ruby
class C
    def a_method
        "C#a_method()"
    end
end

class D < C; end

obj = D.new

#打开单件类定义单件方法
class << obj
    def a_singleton_method
        'obj#a_singleton_method()'
    end
end

obj.singleton_class.superclass  #=> D

```

---

## Ruby对象模型的7条规则



- 只有一个对象 —— 要么是普通对象，要么是模块
- 只有一个模块 —— 可以是一个普通模块、一个类或者一个单件类
- 只有一个方法，它存在于一个模块中 —— 通常是一个类中
- 每个对象（包括类）都有自己的"真正的类"—— 要么是一个普通类，要么是一个单件类
- 除了BasicObject类没有超类外，每个类有且只有一个祖先(superclass)
调用一个方法时，Ruby先向右迈出一步进入接收者真正的类(单件类)，然后向上进入祖先链
---

## 模块与单件类

- 类扩展通过向类的单件类中添加模块来定义类方法。

<aside class="notes">
  上面代码展示了具体类扩展的实现方式，将一个MyModule模块引入到MyClass类的单件类中，因为my_method方法是MyClass的单件类的一个实例方法，这样，my_method方法也是MyClass的一个类方法。

</aside>

```ruby
module MyModule
    def my_method
      "hello"
    end
end

class MyClass
    class << self
        include MyModule
    end
end

MyClass.my_method

```

---

## 对象扩展

- 类方法是单件方法的特例，因此可以把类扩展这种技巧应用到任意对象上，这种技巧即为对象扩展
- 快捷方式Object.extend

```ruby
module MyModule
    def my_method
    end
end

obj = Object.new
class << obj
    include MyModule
end

obj.my_method   # => "hello"
obj.singleton_methods   # => [:my_method]
# 法二：Object#extend方法
module MyModule
    def my_method
    end
end

obj = Object.new
#对象扩展
obj.extend MyModule
obj.my_method  
#类扩展
class MyClass
    extend MyModule
end

MyClass.my_method 

```

---

## 方法包装器

- 方法包装器一般适合于，处理一些你不能直接触碰到的方法，或者需要给某个方法进行一些预处理工作，这个概念有点类似与Python中的装饰器
---

## 方法别名

<aside class="notes">
  
需要注意的是，在顶级作用域中（main）中只能使用alias关键字来命名别名，因为在那里调用不到Module#alias_method方法

此外这里，还需要指出一点关于方法重定义的理解误区，一般我们认为方法一旦被重定义了，就找不回原来的方法了，其实在Ruby中的重定义只是，对方法名与方法实体绑定的一种重新绑定，如果被重新定义的方法体还有一个其它别名，那么一样还是可以访问到老方法的。

</aside>

- alias_method , alias

```ruby
class MyClass
    def my_method
        
    end
    alias_method :m, :my_method
end

obj = MyClass.new
obj.my_method   
obj.m  

```

---

## 环绕别名

- 给方法定义一个别名
- 重定义这个方法
- 在新的方法中调用老的方法

<aside class="notes">
  
上面三步后，即可以保留老方法(第一步)，同时又为原方法增加了新功能。但其本质上没有改变调用之间的函数名称依赖，是一种名副其实的“新瓶装老酒”的取巧办法。

不过环绕别名也有缺点，就是它污染了类的命名空间，添加了额外的方法名。不过这一点其实可以通过Ruby中的private关键字把旧方法限定为私有方法。(Ruby中的public和private实际上针对的是方法名，而非方法本身，言外之意为private方法取个别名，也可以把私有方法暴露出来)

最后要注意的是不要尝试load两次环绕别名的实现代码，否则得到的执行结果就不是你预期中的了，不信你可以试着连续走两遍上面的3个步骤。

</aside>

---

## 细化

- refine

<aside class="notes">
  
前面提到的细化，也可以作为一种方法包装器，在细化的方法中调用super方法，可以调用会细化之前的方法。此外细化相比起环绕别名，细化的作用范围是文件末尾，而环绕别名则是作用在全局。

</aside>

```ruby
module StringRefinement
  refine String do
    def length
      super > 5 ? 'long' : 'short'
    end
  end
end

using StringRefinement

puts "War and Peace".length  

```

---

## 下包含包装器 


<aside class="notes">
  
在介绍祖先链的部分有涉及过include与prepend两个方法，前者是将模块插入到当前类的上方，后者是插入到下方，而下方的位置，正好是方法查找时优先查找的位置，利用这一优势，可以覆写当前类的同名方法，同时通过super关键字还可以调用到该类中的原始方法

</aside>


```ruby
module ExplicitString
    def length
        super > 5 ? ‘long’ : ‘short’
    end
end

String.class_eval do
    prepend ExplicitString
end

puts "War and Peace".length

```

---

## eval方法

- 可以赋予程序在运行中进行动态变化的能力

<aside class="notes">
  Kernal#eval方法与之前的BasicObject#instance_eval和Module#class_eval一样，都属于*eval家族，都可以赋予程序在运行中进行动态变化的能力。与后两者想比Kernal#eval更加直接，不需要代码块、直接就可以执行字符串代码(String of Code)。

PS:BasicObject#instance_eval也是可以执行字符串代码的。

</aside>


```ruby
array = [10, 20]
element = 30
eval("array << element")  #=> [10, 20, 30]
array.instance_eval "self << element"  #=> [10, 20, 30]


```


---

## Here文档(Here documents)

- 以<<打头，后面跟一个__结束序列标识__，之后就可以是正式的文档内容了，可以任意换行，直到遇到了独立出现的__结束序号标识__



```ruby
puts <<GROCERY_LIST
Grocery list
1. Salad mix.
2. Strawberries.*
3. Cereal.
4. Milk.*

* Organic
GROCERY_LIST


```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Grocery list
1. Salad mix.
2. Strawberries.*
3. Cereal.
4. Milk.*

* Organic
=> nil
    </code>
  </pre>

</div>



---

## 绑定对象

- binding


<aside class="notes">
  
  Binding是一个用对象标识的完整作用域(上下文环境)。可以通过创建Binding对象来捕获并带走当前的作用域。之后，通过eval方法在这个Binding对象所携带的作用域内执行代码。
</aside>

```ruby
class MyClass
    def my_method
        @x = 1
        binding
    end
end

b = MyClass.new.my_method
eval "@x", b #=> 1
```

---

## TOPLEVEL_BINDING

<aside class="notes">
  关于绑定还有另外一个知识点，Ruby还提供了一个名为TOPLEVEL_BINDING的预定义常量，表示顶级作用域Binding对象。该常量可以在程序的任何位置访问到。言外之意，你可以在程序的任何位置，通过Kernal#eval方法在顶级作用域中执行代码。

</aside>

```ruby
class AnotherClass
    def my_method
        eval "self", TOPLEVEL_BINDING
    end
end

AnotherClass.new.my_method  #=> main
```

---

## 代码注入

- eval执行这样可以灵活执行字符串代码的特性，给编程带来了灵活性之外，也带来了潜在的风险，如果字符串代码来源于不可信的用户输入，如果不做安全检查，保不齐什么时候就会是一段破坏性的恶意代码

- 面对这样的风险，可以选择规避eval的使用，换用其它相对安全的方式代替,例如动态方法和动态派发。此外，还可以通过在Ruby中通过修改$SAFE全局变量值，来控制程序的安全性级别，具体就是在你要执行可信的字符串代码前，将安全级别降低，可以使用Object#untaint方法，执行完之后在切换安全级别。这有点像操作系统中使用临界资源的步骤(请求锁，释放锁)

- 通过Object#tainted?方法可以判断一个对象是不是被污染了（是否来自一个不可信的输入源）。

---

## 钩子方法

- 钩子方法有些类似事件驱动装置，可以在特定的事件发生后执行特定的回调函数，这个回调函数就是钩子方法(更形象的描述: 钩子方法可以像钩子一样，勾住一个特定的事件。)


<aside class="notes">
  
  通过使用钩子方法，可以让我们在Ruby的类或模块的生命周期中进行干预，可以极大的提高编程的灵活性

</aside>

```ruby
class String
    def self.inherited(subclass)
        puts "#{self} was inherited by #{subclass}"
    end
end
class MyString < String; end
#输出
String was inherited by MyString
```

---

## 类与模块相关

- Class
  * inherited
- Module
  * include, prepended,extend_object
  * method_removed,method_undefined,method_added

---
## demo

```ruby 
module M1 
  def self.included(othermod) 
    puts "M1 was included into #{othermod}"
  end 
end
module M2
  def self.prepended(othermod)
    puts "M2 was prepended to #{othermod}"
  end 
end
class C 
  include M1 
  include M2 
end

```


---

##  单件类相关

- BasicObject#singleton_method_added
- BasicObject#singleton_method_removed
- BasicObject#singleton_method_undefined

```ruby
module M
 def self.method_added(method) 
    puts "New method: M #{method}"
 end

 def my_method
 end 
end

```



