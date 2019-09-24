# Ruby 条件判断



---

## Ruby if...else 语句

- 条件为真执行code
<aside class="notes">
	if 表达式用于条件执行。值 false 和 nil 为假，其他值都为真。请注意，Ruby 使用 elsif，不是使用 else if 和 elif。
如果 conditional 为真，则执行 code。如果 conditional 不为真，则执行 else 子句中指定的 code。
通常我们省略保留字 then 。若想在一行内写出完整的 if 式，则必须以 then 隔开条件式和程式区块

</aside>

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

x=1
if x > 2
   puts "x 大于 2"
elsif x <= 2 and x!=0
   puts "x 是 1"
else
   puts "无法得知 x 的值"
end


```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
x 是 1

    </code>
  </pre>

</div>

---

## Ruby if 修饰符

- 如果 conditional 为真，则执行 code。


```ruby
#!/usr/bin/ruby

$debug=1
print "debug\n" if $debug

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
debug

    </code>
  </pre>

</div>

---

## Ruby unless 语句

- unless式和 if式作用相反，即如果 conditional 为假，则执行 code。如果 conditional 为真，则执行 else 子句中指定的 code。



```ruby
#!/usr/bin/ruby -w
x=1
unless x>2
   puts "x 小于 2"
 else
  puts "x 大于 2"
end


```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
x 小于 2
    </code>
  </pre>

</div>

---

## Ruby unless 修饰符

- 如果 conditional 为假，则执行 code。


```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

$var =  1
print "1 -- 这一行输出\n" if $var
print "2 -- 这一行不输出\n" unless $var

$var = false
print "3 -- 这一行输出\n" unless $var

```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
1 -- 这一行输出
3 -- 这一行输出
    </code>
  </pre>

</div>

---

## Ruby case 语句

- case先对一个 expression 进行匹配判断，然后根据匹配结果进行分支选择

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

$age =  5
case $age
when 0 .. 2
    puts "婴儿"
when 3 .. 6
    puts "小孩"
when 7 .. 12
    puts "child"
when 13 .. 18
    puts "少年"
else
    puts "其他年龄段的"
end

```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
小孩
    </code>
  </pre>

</div>