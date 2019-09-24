# **Ruby 代码块**
---
## 块(block) 概念
- 块是方法的一个重要但非必要的组成部分
- 任何方法后面都可以挂载一个块
- 调用块 
  - yield
  - block.call 方法

---

## demo

<aside class="notes">
  # block is proc
  # &block is block
  # yield和&p的用法
</aside>

```ruby
def meth
end
def block_yield
  puts 'yield'
  yield
end

def block_2 &block
  puts block
  puts 12
  block.call
end
meth { "Where block code live in" }
meth {} {} # => syntax error=
block_yield {puts "12312"}  
block_2 {puts "12312"}
```

---

## Ruby Proc
- block作为参数传入方法后是一个Proc的实例
- block并不依赖proc
- proc可以用&转化成block


---

## Ruby lambda
- lambda是匿名方法
- 在ruby中lambda只能依附proc而存在

--- 


## Proc lamdba 区别

- return 
 - lambda中，return是指从lambda对象返回
 - proc中，return不是从proc返回，而是从定义proc的作用域返回


``` ruby
def another_add()
  my_proc = Proc.new{return 10}
  result = my_proc.call 
  puts "this is unreachable code" 
end
puts another_add  # 10

def add(lam)
   lam.call + 10
end
lam = lambda { return 100 }
puts add(lam) # 110

```


---

## block_given?

- 判断block参数传入

```ruby
def f2(&p)
  puts 'f2'
  p.call if block_given?
end
# f2
# f2 {puts  1233}
```

---

## Proc lamdba 区别

- 检查参数的方式 
 - lambda 参数检查
 - proc 不检查


``` ruby
p = Proc.new { |a,b| [a,b]}
p.call(1,2,3)   #=> [1,2]
p.call(1)      #=> [1, nil]

l = lambda   do  |x , y|
 x + y
end
l.call  1, 2 # 3
l.call  1  # error

```

---

## BEGIN 和 END 块

- 一个程序可以包含多个 BEGIN 和 END 块。
- BEGIN 块按照它们出现的__顺序执行__
- END 块按照它们出现的__相反顺序__执行


---

## 块和方法
- 但是如果方法的最后一个参数前带有 &，那么您可以向该方法传递一个块，且这个块可被赋给最后一个参数
- 如果 * 和 & 同时出现在参数列表中，& 应放在后面。

```
def test(&block)
   block.call
end
test { puts "Hello World!"}

```

---
### lamdba可以和block 一起调用.
```ruby
def meth(lambda_param)
  yield lambda_param
end

meth(-> (x) { x + x }) {|x| x.call(100) }       # => ???
```

