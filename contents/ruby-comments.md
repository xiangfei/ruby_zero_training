# Ruby 注解

- 注释是在运行时会被忽略的 Ruby 代码内的注释行
---

## 单行注解

- 以 # 字符开始


```ruby
#!/usr/bin/ruby -w

# 这是一个单行注释。

puts "Hello, Ruby!"

```

---

## 多行注解

```ruby
#!/usr/bin/ruby -w

puts "Hello, Ruby!"

=begin
这是一个多行注释。
可扩展至任意数量的行。
但 =begin 和 =end 只能出现在第一行和最后一行。 
=end

```

---

## 伪注解


```ruby
#!/usr/bin/ruby -w


'''
这是一个多行注释。
可扩展至任意数量的行。
'''
puts "Hello, Ruby!"


```
