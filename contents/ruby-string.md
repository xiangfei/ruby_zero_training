# ruby **String**

---
# **String**

 - Ruby 中的 String 对象用于存储或操作一个或多个字节的序列。
 - 单引号字符串
 - 双引号字符串
 - 字符编码
 - unpack
---

# 单引号字符串
- 最简单的字符串是单引号字符串，即在单引号内存放字符串：
- %q 使用的是单引号引用规则
```ruby
  desc2 = %q|Ruby 的字符串可以使用 '' 和 ""。|
  '这是一个 Ruby 程序的字符串'
```
- <div style="font-size: 20px">如果您需要在单引号字符串内使用单引号字符，那么需要在单引号字符串使用反斜杠(\)，这样 Ruby 解释器就不会认为这个单引号字符是字符串的终止符号：</div>

```ruby
'Won\'t you read O\'Reilly\'s book?'
```
---
# 双引号字符串
- 在双引号字符串中我们可以使用 #{} 井号和大括号来计算表达式的值：
- 支持更多的转义字符
-  %Q 是双引号引用规则
```ruby
desc1 = %Q{Ruby 的字符串可以使用 '' 和 ""。}
name1 = "Joe"
name2 = "Mary"
puts "你好 #{name1},  #{name2} 在哪?"
```

---
# 字符串编码
- Ruby 的默认字符集是 ASCII，字符可用单个字节表示。如果您使用 UTF-8 或其他现代的字符集，字符可能是用一个到四个字节表示。
- 您可以在程序开头使用 $KCODE 改变字符集，如下所示：

```
$KCODE = 'u'
```
---

#### 下面是 $KCODE 可能的值。

|编码 | 描述|
|:----:|:----:|
|a | ASCII （与 none 相同）。这是默认的。|
|e | EUC。|
|n | None （与 ASCII 相同）。|
|u | UTF-8。|

---
#### 字符串unpack指令
- string to array

```ruby
"abc abc ".unpack('A6Z6')           #=> ["abc", "abc "]
"abc ".unpack('a3a3')               #=> ["abc", " 0000"]
"abc abc ".unpack('Z*Z*')           #=> ["abc ", "abc "]
"aa".unpack('b8B8')                 #=> ["10000110", "01100001"]
"aaa".unpack('h2H2c')               #=> ["16", "61", 97]
"\xfe\xff\xfe\xff".unpack('sS')     #=> [-2, 65534]
"now=20is".unpack('M*')             #=> ["now is"]
"whole".unpack('xax2aX2aX1aX2a')    #=> ["h", "e", "l", "l", "o"]

``` 
---

# **String** 常用内置命令
---

##String 拼接
```ruby
"Ho! " * 3     #=> "Ho! Ho! Ho! "
"Ho! " * 0     #=> ""

a = "hello "
a << "world"   #=> "hello world"
a.concat(33)   #=> "hello world!"
```
---

##String 转换 **Array**
```ruby
"qixi".chars                           #=>["q", "i", "x", "i"]
"hello".each_char {|c| print c, ' ' }  #=>"hello"
```
---
## String 替换 **gsub**/sub
```ruby
"hello".gsub(/[aeiou]/, '*')             #=> "h*ll*"
"hello".gsub(/([aeiou])/, '<\1>')
                                         #=> "h<e>ll<o>"
"hello".gsub(/./) {|s| s.ord.to_s + ' '}
                                         #=> "104 101 108 108 111 "
"hello".gsub(/(?<foo>[aeiou])/, '{\k<foo>}')
                                         #=> "h{e}ll{o}"
'hello'.gsub(/[eo]/, 'e' => 3, 'o' => '*')
                                         #=> "h3ll*"
"quick brown fox".gsub(/[aeiou]/) {|vowel| vowel.upcase }
                                         #=> "qUIck brOwn fOx"
```
---

##String 转换 **Symbols**

```ruby
"I am Ruby developer".to_sym  #=> :"I am Ruby developer"
:"I am Ruby developer".to_s   #=> "I am Ruby developer"
```

**尽量使用Symbol!**

- 不可改变
- 性能更高

---

##**转换 数字**
```ruby

#to complex
'-3/2'.to_c              #=> ((-3/2)+0i)
'-i'.to_c                #=> (0-1i)

#to float
"123.45e1".to_f          #=> 1234.5
"45.67 degrees".to_f     #=> 45.67

#to fixnum
"1100101".to_i(8)        #=> 294977
"99 red balloons".to_i   #=> 99

##fixnum to string
123.to_s(2)              #=> "1111011"
```
