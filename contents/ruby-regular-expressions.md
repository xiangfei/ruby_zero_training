#  Ruby 正则表达式

---

## Ruby 正则表达式

- 正则表达式是一种特殊序列的字符，它通过使用有专门语法的模式来匹配或查找其他字符串或字符串集合。

---

<aside class="notes">
Ruby对正则表达式支持非常好，下面将对我经常使用到的做一个总结，包括Ruby中正则的写法，匹配的方法，替换，分组匹配等。

</aside>


## 语法
- Ruby中正则表达式的写法
 - /pattern/ 要进行转义
 - 在%r{}内 不用进行转义
 - Regexp.new()不用进行转义

```
#!/usr/bin/ruby

line1 = "Cats are smarter than dogs";
line2 = "Dogs also like meat";

if ( line1 =~ /Cats(.*)/ )
  puts "Line1 contains Cats"
end
if ( line2 =~ /Cats(.*)/ )
  puts "Line2 contains  Dogs"
end

```

---

## 正则表达式修饰符
<aside class="notes">
	正则表达式从字面上看可能包含一个可选的修饰符，用于控制各方面的匹配。修饰符在第二个斜杠字符后指定，如上面实例所示。下标列出了 可能的修饰符：

就像字符串通过 %Q 进行分隔一样，Ruby 允许您以 %r 作为正则表达式的开头，后面跟着任意分隔符。这在描述包含大量您不想转义的斜杠字符时非常有用。



</aside>

修饰符	|描述
:--:|:--:
i	|当匹配文本时忽略大小写。
o	|只执行一次 #{} 插值，正则表达式在第一次时就进行判断。
x	|忽略空格，允许在正则表达式中进行注释。
m	|匹配多行，把换行字符识别为正常字符。
u,e,s,n	|把正则表达式解释为 Unicode,EUC,SJIS, 或ASCII

---


<aside class="notes">
	除了控制字符，(+ ? . * ^ $ ( ) [ ] { } | \)，其他所有字符都匹配本身。您可以通过在控制字符前放置一个反斜杠来对控制字符进行转义。

下表列出了 Ruby 中可用的正则表达式语法。

</aside>

## 正则表达式模式
- ^ 开头  
- re* 零次或多次
- $ 结尾 
- re+ 一次或多次
- re? 零次或一次
- re{ n} 表达式 n 次
- a| b 匹配 a 或 b
* re{n,m}  重复n到m次，但尽可能少重复
* re{n,}   重复n次以上，但尽可能少重复
- ...

---

# 正则表达式实例

---

## 字符


```ruby 
/ruby/	#匹配 "ruby"
¥	#匹配 Yen 符号。Ruby 1.9 和 Ruby 1.8 支持多个字符。
```
---

## 字符类


```ruby
/[Rr]uby/	#匹配 "Ruby" 或 "ruby"
/rub[ye]/	#匹配 "ruby" 或 "rube"
/[aeiou]/	#匹配任何一个小写元音字母
/[0-9]/	#匹配任何一个数字，与 /[0123456789]/ 相同
/[a-z]/	#匹配任何一个小写 ASCII 字母
/[A-Z]/	#匹配任何一个大写 ASCII 字母
/[a-zA-Z0-9]/	#匹配任何一个括号内的字符
/[^aeiou]/	#匹配任何一个非小写元音字母的字符
/[^0-9]/	#匹配任何一个非数字字符

```
---

## 特殊字符类


```ruby
/./	 #匹配除了换行符以外的其他任意字符
/./m	#在多行模式下，也能匹配换行符
/\d/	#匹配一个数字，等同于 /[0-9]/
/\D/	#匹配一个非数字，等同于 /[^0-9]/
/\s/	#匹配一个空白字符，等同于 /[ \t\r\n\f]/
/\S/	#匹配一个非空白字符，等同于 /[^ \t\r\n\f]/
/\w/	#匹配一个单词字符，等同于 /[A-Za-z0-9_]/
/\W/	#匹配一个非单词字符，等同于 /[^A-Za-z0-9_]/

```
---

## 重复

```ruby

/ruby?/	#匹配 "rub" 或 "ruby"。其中，y 是可有可无的。
/ruby*/	#匹配 "rub" 加上 0 个或多个的 y。
/ruby+/	#匹配 "rub" 加上 1 个或多个的 y。
/\d{3}/	#刚好匹配 3 个数字。
/\d{3,}/	#匹配 3 个或多个数字。
/\d{3,5}/	#匹配 3 个、4 个或 5 个数字。
```
---

##  贪婪/非贪婪匹配

```ruby
/<.*>/	#贪婪重复：匹配 "<ruby>perl>"
/<.*?>/	#非贪婪重复：匹配 "<ruby>perl>" 中的 "<ruby>"
```
---

## 通过圆括号进行分组

```ruby
/\D\d+/	 #无分组： + 重复 \d
/(\D\d)+/	#分组： + 重复 \D\d 对
/([Rr]uby(, )?)+/	#匹配 "Ruby"、"Ruby, ruby, ruby"，等等

```
---

## 反向引用

```ruby
/([Rr])uby&\1ails/	#匹配 ruby&rails 或 Ruby&Rails
/(['"])(?:(?!\1).)*\1/	#单引号或双引号字符串。\1 匹配第一个分组所匹配的字符，\2 匹配第二个分组所匹配的字符，依此类推。
```
---

## 替换


```ruby
/ruby|rube/	#匹配 "ruby" 或 "rube"
/rub(y|le))/	#匹配 "ruby" 或 "ruble"
/ruby(!+|\?)/	#{}"ruby" 后跟一个或多个 ! 或者跟一个 ?
```
---

## 锚


```ruby
/^Ruby/	#匹配以 "Ruby" 开头的字符串或行
/Ruby$/	#匹配以 "Ruby" 结尾的字符串或行
/\ARuby/	#匹配以 "Ruby" 开头的字符串
/Ruby\Z/	#匹配以 "Ruby" 结尾的字符串
/Ruby/	#匹配单词边界的 "Ruby"
/rub\B/	#\B 是非单词边界：匹配 "rube" 和 "ruby" 中的 "rub"，但不匹配单独的 "rub"
/Ruby(?=!)/	#如果 "Ruby" 后跟着一个感叹号，则匹配 "Ruby"
/Ruby(?!!)/	#如果 "Ruby" 后没有跟着一个感叹号，则匹配 "Ruby"

```

---
## 圆括号的特殊语法


```ruby
/R(?#comment)/	#匹配 "R"。所有剩余的字符都是注释。
/R(?i)uby/	#当匹配 "uby" 时不区分大小写。
/R(?i:uby)/	#与上面相同。
/rub(?:y|le))/	#只分组，不进行 \1 反向引用
```

---

##  匹配的写法

 - =~ 肯定匹配 
 - !~ 否定匹配
 - regexp#match(str)，返回MatchData，一个数组，从0开始，还有match.pre_match返回匹配前内容，match.post_match返回匹配后内容

```ruby
/cat/ =~ "dog and cat" 	#返回8
mt = /cat/.match("bigcatcomes")
"#{mt.pre_match}->#{mt[0]}<-#{mt.post_match}" #返回big->cat<-comes

```

---

##  替换

<aside class="notes">
很多时候匹配是为了替换，Ruby中进行正则替换非常简单，两个方法即可搞定，sub()+gsub()。
sub只替换第一次匹配，gsub（g:global）会替换所有的匹配，没有匹配到返回原字符串的copy
</aside>


```ruby
str = "ABDADA"
new_str = str.sub(/A/, "*") 	#返回"*BDADA"
new_str2 = str.gsub(/A/, "*")	#返回"*BD*D*"
```

如果想修改原始字符串用sub!()和gsub!()，没有匹配到返回nil。

方法后面还可以跟block，对匹配的字符串进行操作
```ruby
a.gsub(/[aeiou]/) {|vowel| vowel.upcase } # => "qUIck brOwn fOx"
```

--- 

## 分组匹配
Ruby的分组匹配与其它语言差别不大，分组匹配表达式是对要进行分组的内容加()。

对于匹配到的结果，可以用系统变量#$1，#$2…索引，也可用matchData数组来索引
```ruby
md = /(\d\d):(\d\d)(..)/.match("12:50am") # md为一个MatchData对象
puts "Hour is #$1, minute #$2"
puts "Hour is #{md[1]}, minute #{md[2]}"
```

--- 

## 匹配所有

- regexp#match()只能匹配一次，如果想匹配所有要用regexp#scan()

```
"abcabcabz".scan(%r{abc}).each {|item| puts item} # 输出2行abc
```
