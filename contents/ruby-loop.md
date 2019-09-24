# Ruby 循环



---

## Ruby while 语句
- 当 conditional 为真时，执行 code。
<aside class="notes">
	语法中 do 或 : 可以省略不写。但若要在一行内写出 while 式，则必须以 do 或 : 隔开条件式或程式区块。

</aside>

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-
$i = 0
$num = 5
while $i < $num  do
   puts("在循环语句中 i = #{$i}" )
   $i +=1
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Inside the loop i = 0
Inside the loop i = 1
Inside the loop i = 2
Inside the loop i = 3
Inside the loop i = 4
    </code>
  </pre>

</div>

---

## Ruby while 修饰符

- 如果 conditional 为真，则执行 code。

<aside class="notes">
  如果 while 修饰符跟在一个没有 rescue 或 ensure 子句的 begin 语句后面，code 会在 conditional 判断之前执行一次
</aside>

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-
$i = 0
$num = 5
begin
   puts("在循环语句中 i = #{$i}" )
   $i +=1
end while $i < $num
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
在循环语句中 i = 0
在循环语句中 i = 1
在循环语句中 i = 2
在循环语句中 i = 3
在循环语句中 i = 4
    </code>
  </pre>

</div>

---

## Ruby until 语句
- 当 conditional 为假时，执行 code


```ruby
#!/usr/bin/ruby -w
$i = 0
$num = 5
until $i > $num  do
   puts("在循环语句中 i = #{$i}" )
   $i +=1;
end
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
在循环语句中 i = 0
在循环语句中 i = 1
在循环语句中 i = 2
在循环语句中 i = 3
在循环语句中 i = 4
在循环语句中 i = 5
    </code>
  </pre>

</div>

---

## Ruby until 修饰符

- 如果 conditional 为假，则执行 code。


```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-
$i = 0
$num = 5
begin
   puts("在循环语句中 i = #{$i}" )
   $i +=1;
end until $i > $num
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
在循环语句中 i = 0
在循环语句中 i = 1
在循环语句中 i = 2
在循环语句中 i = 3
在循环语句中 i = 4
在循环语句中 i = 5
    </code>
  </pre>

</div>

---

## Ruby for 语句

- 针对 expression 中的每个元素分别执行一次 code。

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-
for i in 0..5
   puts "局部变量的值为 #{i}"
end
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
局部变量的值为 0
局部变量的值为 1
局部变量的值为 2
局部变量的值为 3
局部变量的值为 4
局部变量的值为 5
    </code>
  </pre>

</div>

--- 

## Ruby break 语句

- 终止最内部的循环。如果在块内调用，则终止相关块的方法

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

for i in 0..5
   if i > 2 then
      break
   end
   puts "局部变量的值为 #{i}"
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
局部变量的值为 0
局部变量的值为 1
局部变量的值为 2
    </code>
  </pre>

</div>

---

## Ruby next 语句

- 跳到最内部循环的下一个迭代。如果在块内调用，则终止块的执行

```ruby
for i in 0..5
   if i < 2 then
      next
   end
   puts "局部变量的值为 #{i}"
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
局部变量的值为 2
局部变量的值为 3
局部变量的值为 4
局部变量的值为 5
    </code>
  </pre>

</div>

---

## Ruby redo
- 重新开始最内部循环的该次迭代，不检查循环条件。如果在块内调用，则重新开始 yield 或 call。

```ruby
for i in 0..5
   if i < 2 then
      puts "局部变量的值为 #{i}"
      redo
   end
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
局部变量的值为 0
局部变量的值为 0
............................
    </code>
  </pre>

</div>

---
## Ruby retry

- 如果 retry 出现在 begin 表达式的 rescue 子句中，则从 begin 主体的开头重新开始
- 如果 retry 出现在迭代内、块内或者 for 表达式的主体内，则重新开始迭代调用。迭代的参数会重新评估

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

for i in 1..5
   retry if  i > 2
   puts "局部变量的值为 #{i}"
end

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
局部变量的值为 1
局部变量的值为 2
............................
    </code>
  </pre>

</div>