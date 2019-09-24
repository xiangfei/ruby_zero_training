# Ruby 文件的输入与输出


---
- Ruby 提供了一整套 I/O 相关的方法，在内核（Kernel）模块中实现。所有的 I/O 方法派生自 IO 类。
- 类 IO 提供了所有基础的方法，比如 read、 write、 gets、 puts、 readline、 getc 和 printf。


---

## puts 语句

- 您赋值给变量，然后使用 puts 语句打印输出
- 语句在输出内容后会跳到下一行
```ruby
#!/usr/bin/ruby
val1 = "This is variable one"
puts val1
```
---

## gets 语句
- gets 语句可用于获取来自名为 STDIN 的标准屏幕的用户输入。

```ruby
#!/usr/bin/ruby

puts "Enter a value :"
val = gets
puts val
```
---

## print 语句

- print 输出光标定位在同一行。


```ruby
#!/usr/bin/ruby

print "Hello World"
print "Good Morning"
```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">

Hello WorldGood Morning

    </code>
  </pre>

</div>

---

## 打开和关闭文件

- File.open
 - key和块关联 
- File.new
 - 需要关闭文件 


```ruby
aFile = File.new("filename", "mode")
   # ... 处理文件
aFile.close

File.open("filename", "w+") do |aFile|
   # ... process the file
end

```

---

## 读取和写入文件


```ruby
# read
aFile = File.new("input.txt", "r")
if aFile
   content = aFile.sysread(20)
   puts content
else
   puts "Unable to open file!"
end
aFile.close
# write

aFile = File.new("input.txt", "w+")
if aFile
   aFile.syswrite("ABCDEF")
else
   puts "Unable to open file!"
end
aFile.close
```
---

## 重命名和删除文件


```ruby
File.rename( "test1.txt", "test2.txt" )
File.delete("text2.txt")

```

---


## 文件模式与所有权

```ruby
file = File.new( "test.txt", "w" )
file.chmod( 0755 )
```
- 0700	rwx 掩码，针对所有者
- 0400	r ，针对所有者
- 0200	w ，针对所有者
- 0100	x ，针对所有者
- 0070	rwx 掩码，针对所属组
- 0040	r ，针对所属组
- 0020	w ，针对所属组
- 0010	x ，针对所属组
- 0007	rwx 掩码，针对其他人
- 0004	r ，针对其他人
- 0002	w ，针对其他人
- 0001	x ，针对其他人
- 4000	执行时设置用户 ID
- 2000	执行时设置所属组 ID
- 1000	保存交换文本，甚至在使用后也会保存

---

## 文件查询


```ruby
File.file?( "text.txt" ) #文件
File::directory?( "/usr/local/bin" ) #目录
```

---

# Ruby 中的目录

---

## 浏览目录

```ruby
Dir.chdir("/usr/bin")
Dir.entries("/usr/bin").join(' ')

```

---
## 创建/删除目录

```ruby 
Dir.mkdir("mynewdir" , mod)
Dir.delete("testdir")


```
