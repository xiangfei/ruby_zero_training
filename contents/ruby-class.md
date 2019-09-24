# Ruby 类和对象

---
## Ruby 类和对象


Ruby 是一种完美的面向对象编程语言。
面向对象编程语言的特性包括

- 数据封装
- 数据抽象
- 多态性
- 继承


<aside class="notes">
一个面向对象的程序，涉及到的类和对象。类是个别对象创建的蓝图。在面向对象的术语中，您的自行车是自行车类的一个实例。

以车辆为例，它包括车轮（wheels）、马力（horsepower）、燃油或燃气罐容量（fuel or gas tank capacity）。这些属性形成了车辆（Vehicle）类的数据成员。借助这些属性您能把一个车辆从其他车辆中区分出来。

车辆也能包含特定的函数，比如暂停（halting）、驾驶（driving）、超速（speeding）。这些函数形成了车辆（Vehicle）类的数据成员。因此，您可以定义类为属性和函数的组合。
</aside>
---

## 在 Ruby 中定义类

- 类总是以关键字 class 开始
- 类名的首字母应该大写
- end 结尾

```ruby 
class Customer
end
```



---

## Ruby 类中的对象
- Ruby中使用new方法创建对象
  - new方法是一种独特的方法，这是预定义在Ruby库
- 对象是类的实例
---

### 创建对象
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
cust1=Customer.new
    </code>
  </pre>
</div>
---

### 自定义方法来创建Ruby对象
- 可以通过new方法的参数，这些参数可以用来初始化类变量
- 当打算声明的new方法具有参数，需要声明的方法在创建类的时候初始化
- initialize方法是一种特殊类型的方法，该方法时将执行new方法的类被称为参数



```ruby
class Customer
  @@no_of_customers=0
  def initialize(id,name,addr)
    @cust_id=id
    @cust_name=name
    @cust_addr=addrendend
  end
end
#创建对象
cust1=Customer.new("1" , "xx" , "zz")
```


<aside class="notes">
  在这个例子中，可以声明局部变量的初始化方法id,name和addr
这里def结束被用来定义一个Ruby的方法初始化。这些将在有关后续章节中了解更多。
在initialize方法中，对这些局部变量的值传递到实例变量
@cust_id,@cust_name和@cust_addr。
这里的局部变量持有的值由new方法一同传递

</aside>


---

### Ruby 类中的成员函数

- 在Ruby中函数被称为方法
- 以关键字 __def__ 开始 __end__ 结束 后跟方法名
- 方法名总是以小写字母开头




```
class Sample
   def function
      statement 1
      statement 2
   end
end

```


<aside class="notes">
在这里，statement 1 和 statement 2 是类 Sample 内的方法 function 的主体的组成部分
这些语句可以是任何有效的 Ruby 语句
</aside> 



--- 

### ruby class Demo

  创建一个名为 Customer 的 Ruby 类,声明两个方法

- display_details
 - 该方法用于显示客户的详细信息
- total_no_of_customers
 - 该方法用于显示在系统中创建的客户总数量



```ruby
#!/usr/bin/ruby

class Customer

  @@no_of_customers=0
  def initialize (id,name,addr)
    @cust_id=id
    @cust_name=name
    @cust_addr=addr
  end
  def display_details()
    puts "Customer id #@cust_id"
    puts "Customer name #@cust_name"
    puts "Customer address #@cust_addr"
  end
  def total_no_of_customers()
    @@no_of_customers += 1
    puts "Total number of customers: #@@no_of_customers"
  end
end

```

<aside class="notes">
<p>将在一个单行上显示文本 Customer id，后跟变量 @cust_id 的值。</p>

<p>当您想要在一个单行上显示实例变量的文本和值时，您需要在 puts 语句的变量名前面放置符号（#）。文本和带有符号（#）的实例变量应使用双引号标记。</p>

<p>第二个方法，total_no_of_customers，包含了类变量 @@no_of_customers。表达式 @@no_of_ customers+=1 在每次调用方法 total_no_of_customers 时，把变量 no_of_customers 加 1。通过这种方式，您将得到类变量中的客户总数量。</p>
<p>在这里，我们创建了 Customer 类的两个对象，cust1 和 cust2，并向 new 方法传递必要的参数。当 initialize 方法被调用时，对象的必要属性被初始化。</p>

<p>一旦对象被创建，您需要使用两个对象来调用类的方法。如果您想要调用方法或任何数据成员，您可以编写代码，</p>
</aside> 



