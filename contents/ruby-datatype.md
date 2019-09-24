# ruby **数据类型**

- Number
- String
- Ranges
- Symbols
- true
- false
- **array**
- **hash**
---


## 数值类型(Number)

- 整型(Integer)

<aside class="notes">
  整型分两种，如果在31位以内（四字节），那为Fixnum实例。如果超过，即为Bignum实例。
  整数范围从 -230 到 230-1 或 -262 到 262-1。在这个范围内的整数是类 Fixnum 的对象，在这个范围外的整数存储在类 Bignum 的对象中。

您可以在整数前使用一个可选的前导符号，一个可选的基础指标（0 对应 octal，0x 对应 hex，0b 对应 binary），后跟一串数字。下划线字符在数字字符串中被忽略。

您可以获取一个 ASCII 字符或一个用问号标记的转义序列的整数值。
</aside>


```ruby
# Fixnum 十进制
123
# Fixnum 带有下划线的十进制
1_234
# 负的 Fixnum
-500
# 八进制
0377
# 十六进制
0xff
# 二进制
0b1011
# 'a' 的字符编码
?a
# 换行符（0x0a）的编码
?\n
# Bignum
12345678901234567890 

```

---


## 浮点型Float

<aside class="notes">
  Ruby 支持浮点数。它们是带有小数的数字。浮点数是类 Float 的对象，且可以是下列中任意一个。

</aside>

```ruby
123.4# 浮点值
1.0e6# 科学记数法
4E20# 不是必需的
4e+20# 指数前的符号

```
---
## 算术操作

- 加减乘除操作符：+-*/；指数操作符为**
- 指数不必是整数

```ruby
#指数算术 
puts 2**(1/4)#1与4的商为0，然后2的0次方为1 
puts 16**(1/4.0)#1与4.0的商为0.25（四分之一），然后开四次方根 
```
--- 
## String 类型
- Ruby 字符串简单地说是一个 8 位字节序列，它们是类 String 的对象
- 双引号标记的字符串允许替换和使用反斜线符号，单引号标记的字符串不允许替换，且只允许使用 \\\\ 和 \' 两个反斜线符号
- 您可以使用序列 #{ expr } 替换任意 Ruby 表达式的值为一个字符串
```ruby
puts 'escape using "\\"';
puts 'That\'s right';
puts "Multiplication Value : #{24*60*60}";
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
escape using "\"
That's right
Multiplication Value : 86400
    </code>
  </pre>

</div>

--- 

## Array 类型

数组字面量通过[]中以逗号分隔定义，且支持range定义。

- 数组通过[]索引访问
- 通过赋值操作插入、删除、替换元素
- 通过+，－号进行合并和删除元素，且集合做为新集合出现
- 通过<<号向原数据追加元素
- 通过*号重复数组元素
- 通过｜和&符号做并集和交集操作（注意顺序）

```
ary = [ "fred", 10, 3.14, "This is a string", "last element", ]
ary.each do |i|
    puts i
end
```
---

## Hash 类型

- Ruby 哈希是在大括号内放置一系列键/值对，键和值之间使用逗号和序列 => 分隔。尾部的逗号会被忽略。

```ruby 
#!/usr/bin/ruby

hsh = colors = { "red" => 0xf00, "green" => 0x0f0, "blue" => 0x00f }
hsh.each do |key, value|
    print key, " is ", value, "\n"
end


```
---

## Range 类型

- s..e 
- s...e 
- Range.new

<aside class="notes">
  一个范围表示一个区间。

范围是通过设置一个开始值和一个结束值来表示。范围可使用 s..e 和 s...e 来构造，或者通过 Range.new 来构造。
使用 .. 构造的范围从开始值运行到结束值（包含结束值）。使用 ... 构造的范围从开始值运行到结束值（不包含结束值）。当作为一个迭代器使用时，范围会返回序列中的每个值。

范围 (1..5) 意味着它包含值 1, 2, 3, 4, 5，范围 (1...5) 意味着它包含值 1, 2, 3, 4 。

</aside>

```ruby 
#!/usr/bin/ruby

(10..15).each do |n|
    print n, ' '
end

```

