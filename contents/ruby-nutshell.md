# **Ruby** 并行编程

---
## 设计模式定义
- 设计模式是程序术语,设计上经常反复使用的模式
- 程序抽象化的延伸
 - 继承是把单一类的公共部分抽象化,达到重复利用

--- 
## Ruby 设计模式

---
## singleton 模式

- 使用类库

```ruby
   require 'singleton'

   class Example
     include Singleton
     attr_accessor :keep, :strip
     def _dump(depth)
       # this strips the @strip information from the instance
       Marshal.dump(@keep, depth)
     end

     def self._load(str)
       instance.keep = Marshal.load(str)
       instance
     end
   end

   a = Example.instance
   a.keep = "keep this"
   a.strip = "get rid of this"
   a.taint

   stored_state = Marshal.dump(a)

   a.keep = nil
   a.strip = nil
   b = Marshal.load(stored_state)
   p a == b  #  => true
   p a.keep  #  => "keep this"
   p a.strip #  => nil


```
---
## singleton 模式

- 使用类

```ruby
class Example

  def self.instance
  	return "xxx"
  end

end

```
--- 
## singleton 模式

- 使用固定变量

```ruby
class Example
 
  def instance
     return ""
  end


end
Test = Example.new
Test.instance
```
---

## singleton 模式

- 使用特殊类

```ruby
Example = Object.new
 
 def Example.spool
    return ""

 end

Example.spool
```


---

## Proxy 模式

- 使用delegate 库

```ruby
require 'delegate'
  class Tempfile < DelegateClass(File)
    # constant and class member data initialization...

    def initialize(basename, tmpdir=Dir::tmpdir)
      # build up file path/name in var tmpname...

      @tmpfile = File.open(tmpname, File::RDWR|File::CREAT|File::EXCL, 0600)

      # ...

      super(@tmpfile)

      # below this point, all methods of File are supported...
    end

    # ...
  end

```


---

## Proxy 模式

- 使用delegate 库

```ruby
  class Stats
    def initialize
      @source = SimpleDelegator.new([])
    end

    def stats(records)
      @source.__setobj__(records)

      "Elements:  #{@source.size}\n" +
      " Non-Nil:  #{@source.compact.size}\n" +
      "  Unique:  #{@source.uniq.size}\n"
    end
  end

  s = Stats.new
  puts s.stats(%w{James Edward Gray II})
  puts
  puts s.stats([1, 2, 3, nil, 4, 5, 1, 2])

```

---

## Proxy 模式

- 使用类

```ruby
class Proxy

  def initialize obj
  	@obj  = obj
  end

  def method_missing name , *args
     @obj.send name , *args
  end
end


```

---

## iterator 模式

- 按顺序访问集合对象的方法
- 为集合对象另外准备用来控制循环处理的对象
---
## ruby iterator

- ruby迭代通过块处理的,使用块进行循环的抽象对象属于访问者模式

---
## 外部迭代器

- 需要引用集合对象内部的信息
- 破坏了集合内部的封装性原则,因为类和迭代器紧密的联系在一起

```ruby

class ArrayIterator 
	attr_accessor :current

	def initialize array
       @arr = array
       self.current = 0
	end

	def first
		 self.current = 0
	end

	def next
 		self.current =  self.current + 1
 	end

	def done?
		return self.current >= @arr.size
	end

	def current_item
		return @arr[self.current]
	end
end

a = ArrayIterator.new [1,2,3,4]

until a.done?
 p a.next
end

```

---

## 内部迭代器

- 不能同时进行多个循环
- 无法按照顺序比较2个集合的元素

```ruby
[1,2,3,4].each do |a|
 p a
end

```
---
##  迭代器比较

```ruby
#无法实现多个数组并列处理
a = [1,2,3]
b = [9,8,7]
result = []
0.upto 2 do  |i| 
	result <<  a[i]
	result << b[i]
	i = i + 1
end

p result

# 外部迭代器
result = []
a = ArrayIterator.new [1, 2, 3]
b = ArrayIterator.new [9, 8, 7]
until a.done? or b.done?
  result << a.current_item
  a.next
  result << b.current_item
  b.next
end
p result

```

---

## Prototype 模式

- 明确一个实例作为要生成对象的种类原型
- 通过复制该实例在生成新的对象

---

## ruby中的原型

- 复制对象的clone方法
- 给个别对象增加方法

```ruby
object = Object.new
dog = object.clone 

def dog.sit
puts "sit"
end

puts dog.sit

```

---

## Template 模式

- 在父类方法中定义算法的框架
- 其中几个步骤的具体实现内容留给子类实现

---
##  ruby Template 模式

- 最大灵活运用 template模式的是Enumerable Comparable模块

```ruby
dice  = Object.new

def dice.each

   10.times do 
   	  yield rand(6) + 1
   end
end

dice.extend Enumerable
#排除 3 以下的整数
p dice.reject {|x| x< 3}

```

---

## Observer 模式

- 当一个对象发生变化时,依赖该对象的全部对象自动得到通知

---


## Ruby Observer 模式

- 提供了observer 模块
 - 观察者类(被观察者类)不必是特定类的子类
 - 观察者类更新方法名(参数)可以自有指定
 - 被观察者类 引入Observer模块

``` ruby
  require "observer"

  class Ticker          ### Periodically fetch a stock price.
    include Observable

    def initialize(symbol)
      @symbol = symbol
    end

    def run
      last_price = nil
      loop do
        price = Price.fetch(@symbol)
        print "Current price: #{price}\n"
        if price != last_price
          changed                 # notify observers
          last_price = price
          notify_observers(Time.now, price)
        end
        sleep 1
      end
    end
  end

  class Price           ### A mock class to fetch a stock price (60 - 140).
    def self.fetch(symbol)
      60 + rand(80)
    end
  end

  class Warner          ### An abstract observer of Ticker objects.
    def initialize(ticker, limit)
      @limit = limit
      ticker.add_observer(self)
    end
  end

  class WarnLow < Warner
    def update(time, price)       # callback for observer
      if price < @limit
        print "--- #{time.to_s}: Price below #@limit: #{price}\n"
      end
    end
  end

  class WarnHigh < Warner
    def update(time, price)       # callback for observer
      if price > @limit
        print "+++ #{time.to_s}: Price above #@limit: #{price}\n"
      end
    end
  end

  ticker = Ticker.new("MSFT")
  WarnLow.new(ticker, 80)
  WarnHigh.new(ticker, 120)
  ticker.run

Produces:

  Current price: 83
  Current price: 75
  --- Sun Jun 09 00:10:25 CDT 2002: Price below 80: 75
  Current price: 90
  Current price: 134
  +++ Sun Jun 09 00:10:25 CDT 2002: Price above 120: 134
  Current price: 134
  Current price: 112
  Current price: 79
  --- Sun Jun 09 00:10:25 CDT 2002: Price below 80: 79

```
---
# OCP 软件开放封闭原则

- 对模块扩展必须开放
- 对修改必须封闭

```ruby
box1 = Object.new
box2 = Object.new
box3 = Object.new

def box1.open
   puts "open box1"
end

def box2.open
   puts "open box2"
end

def box3.open
   puts "open box3"
end
# 3个箱子是不同的对象，打开箱子需调用box open
# 实现，程序的子类 * 箱子的种类

def open_box box
    if box.type == "box1"
    	puts "open box1"
    elsif box.type == "box2"
    	puts "open box2"
    elsif box.type == "box3"
    	puts "open box3"
    else
    	puts "unkonwn function"
    end
end
```

---

strategy 模式