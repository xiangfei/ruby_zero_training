# Ruby 变量


---
<aside class="notes">
  
  变量是持有可被任何程序使用的任何数据的存储位置。

</aside>

## Ruby 支持五种类型的变量。

- 局部变量
- 实例变量
- 类变量
- 全局变量
- 常量

---

## Ruby 全局变量
- 以 $ 开头
- 未初始化的全局变量的值为 nil
- 在使用 -w 选项后，会产生警告

```ruby

#!/usr/bin/ruby

$global_variable = 10
class Class1
  def print_global
     puts "Global variable in Class1 is #{$global_variable}"
  end
end

class1obj = Class1.new
class1obj.print_global

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Global variable in Class1 is 10
    </code>
  </pre>
</div>

---
## Ruby 实例变量

- @ 开头
- 未初始化的实例变量的值为 nil


```ruby 
#!/usr/bin/ruby
class Customer
   def initialize id
      @cust_id=id
   end
   def display_details()
      puts "Customer id #@cust_id"
    end
end
# 创建对象
cust1=Customer.new "1"
# 调用方法
cust1.display_details()
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Customer id 1
    </code>
  </pre>
</div>

---
## Ruby 类变量

- @@ 开头
- 未初始化的报错


```ruby
class Customer
   @@no_of_customers=0
    def total_no_of_customers()
       @@no_of_customers += 1
       puts "Total number of customers: #@@no_of_customers"
    end
end
# 创建对象
cust1=Customer.new
cust2=Customer.new
# 调用方法
cust1.total_no_of_customers()
cust2.total_no_of_customers()
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">

Total number of customers: 1
Total number of customers: 2
    </code>
  </pre>
</div>


---

## Ruby 局部变量

 - 以小写字母或下划线 _ 开头。
 - 局部变量的作用域从 class,module ,def , do  ,{}
 - 当调用一个未初始化的局部变量时，它被解释为调用一个不带参数的方法


---

## Ruby 常量

- 常量以大写字母开
- 常量不能定义在方法内



```bash
2.4.2 :053 > class A
2.4.2 :054?>   B = 12
2.4.2 :055?>   def s
2.4.2 :056?>     B = 13
2.4.2 :057?>     end
2.4.2 :058?>   end
SyntaxError: (irb):56: dynamic constant assignment
B = 13


```
---
## Ruby 伪变量

- 不能赋值
<aside class="notes">
  
  它们是特殊的变量，有着局部变量的外观，但行为却像常量。您不能给这些变量赋任何值。

</aside>

- self: 当前方法的接收器对象。
- true: 代表 true 的值。
- false: 代表 false 的值。
- nil: 代表 undefined 的值。
- \__FILE__: 当前源文件的名称。
- \__LINE__: 当前行在源文件中的编号。


