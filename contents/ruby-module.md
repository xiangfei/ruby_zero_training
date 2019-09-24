# Ruby Module

---
## 定义

<aside class="notes">
  
模块（Module）定义了一个命名空间，相当于一个沙盒，在里边您的方法和常量不会与其他地方的方法常量冲突。

</aside>

- 模块（Module）是一种把方法、类和常量组合在一起的方式。模块（Module）为您提供了两大好处。
 - 模块提供了一个命名空间和避免名字冲突。
 - 模块实现了 mixin 装置

- 模块常量命名与类常量命名类似，以大写字母开头
- 方法定义看起来也相似
- 可以使用模块名称和两个冒号来引用一个常量
---

## 模块 类的区别

- 模块不能实例化
- 模块没有子类
- 模块只能被另一个模块定义

---
## Demo

```ruby
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
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :468 > Trig::sin 12
 => nil 
2.4.2 :469 > Trig.sin 12
 => nil 
2.4.2 :470 > Trig::PI
 => 3.141592654 

    </code>
  </pre>

</div>


---

## 模块引入
- 使用include

```bin
2.4.2 :484 > module X
2.4.2 :485?>   def s
2.4.2 :486?>     end
2.4.2 :487?>   end
 => :s 
2.4.2 :488 > X
 => X 
2.4.2 :489 > X.s
2.4.2 :492 > include X
 => Object 
2.4.2 :493 > s
 => nil 

```

---

## Ruby 中的 Mixins

<aside class="notes">
当一个类可以从多个父类继承类的特性时，该类显示为多重继承。

Ruby 不直接支持多重继承，但是 Ruby 的模块（Module）有另一个神奇的功能。它几乎消除了多重继承的需要，提供了一种名为 mixin 的装置。

Mixins 向您提供了一种完美的为类添加功能的控制方式。但是，它们真正的强大在于当 mixin 中的代码开始与使用它的类中的代码交互时。

模块 A 由方法 a1 。
模块 B 由方法 b1 。
类 Sample 包含了模块 A 和 B。
类 Sample 可以访问所有四个方法，即 a1、b1 。
    因此，您可以看到类 Sample 继承了两个模块，您可以说类 Sample 使用了多重继承或 mixin 。

</aside>

```ruby
module A
   def a1
   end
end
module B
   def b1
   end
end

class Sample
include A
include B
   def s1
   end
end

samp=Sample.new
samp.a1
samp.b1
samp.s1
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :521 >   samp=Sample.new
 => #<Sample:0x0000000000edc448> 
2.4.2 :522 > samp.a1
 => nil 
2.4.2 :524 > samp.b1
 => nil 
2.4.2 :526 > samp.s1
 => nil 
    </code>
  </pre>

</div>

