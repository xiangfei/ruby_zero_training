# ruby **语法**

---


## Ruby 语法

- 所有的 Ruby 文件扩展名都是 .rb

--- 

## Ruby 程序中的空白
- 在 Ruby 代码中的空白字符，如空格和制表符一般会被忽略
- 除非当它们出现在字符串中时才不会被忽略
- 用于解释模棱两可的语句。当启用 -w 选项时 这种解释会产生警告

```ruby
a + b 被解释为 a+b （这是一个局部变量）
a  +b 被解释为 a(+b) （这是一个方法调用）

```

---


## Ruby 程序中的行尾
- Ruby 把分号和换行符解释为语句的结尾。
- 但是，如果 Ruby 在行尾遇到运算符，比如 +、- 或反斜杠，它们表示一个语句的延续。

---

## Ruby 标识符
- 标识符是变量、常量和方法的名称
- Ruby 标识符是大小写敏感的
- Ruby 标识符的名称可以包含字母、数字和下划线字符（ _ ）

--- 

## 保留字

|BEGIN |do | next|  then|
|:--:|:--:|:--:|
|END |else | nil |true|
|alias| elsif| not |undef|
|and |end |or|  unless|
|begin |ensure|  redo  |until|
|break |false |rescue  |when|
|case  |for |retry |while|
|class| if | return | while|
|def |in  |self | \__FILE__|
|defined?  |module|  super| \__LINE__|

---

## Ruby 中的 Here Document

- "Here Document" 是指建立多行字符串。在 << 之后

<aside class="notes">
"Here Document" 是指建立多行字符串。在 << 之后，您可以指定一个字符串或标识符来终止字符串，且当前行之后直到终止符为止的所有行是字符串的值。

如果终止符用引号括起，引号的类型决定了面向行的字符串类型。请注意<< 和终止符之间必须没有空格。

</aside> 

```ruby
#!/usr/bin/ruby -w
# -*- coding : utf-8 -*-

print <<EOF
    这是第一种方式创建here document 。
    多行字符串。
EOF

print <<"EOF";                # 与上面相同
    这是第二种方式创建here document 。
    多行字符串。
EOF

print <<`EOC`                 # 执行命令
  echo hi there
  echo lo there
EOC

print <<"foo", <<"bar"        # 您可以把它们进行堆叠
  I said foo.
foo
  I said bar.
bar

```


---

## Ruby BEGIN 语句

- 程序运行之前被调用


```
#!/usr/bin/ruby

puts "This is main Ruby Program"

BEGIN {
   puts "Initializing Ruby Program"
}

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Initializing Ruby Program
This is main Ruby Program
    </code>
  </pre>
</code>

---

## Ruby END 语句

- 在程序的结尾被调用

```ruby
#!/usr/bin/ruby

puts "This is main Ruby Program"

END {
   puts "Terminating Ruby Program"
}
BEGIN {
   puts "Initializing Ruby Program"
}

```


<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Initializing Ruby Program
This is main Ruby Program
Terminating Ruby Program
    </code>
  </pre>
</code>