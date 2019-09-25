# ruby **Array**

---
#**Array** []
- Ruby 数组是任何对象的有序的、整数索引的集合。数组中的每个元素都与一个索引相关，并可通过索引进行获取。
- 数组的索引从 0 开始
- -1 表示数组的最后一个元素，-2 表示数组中的倒数第二个元素，依此类推
- Ruby 数组可存储诸如 String、 Integer、 Fixnum、 Hash、 Symbol ...
- Ruby 数组不像其他语言中的数组那么刚性。当向数组添加元素时,Ruby 数组会自动增长

---
##**Array** 创建

```ruby
names = Array.new  || names = [] #初始化一个数组
names = Array.new(20) #初始化同时设定长度
a = [ 1, "cat", 3.14 ] || a = Array.new [1, "cat", 3.14]  #初始化并赋值

names = Array.new(4, "mac")
# 长度4 ,每一个值是mac ["mac", "mac", "mac", "mac"] 
asci = Array('a'..'z')
digits = Array(0..9)

```
---

##Array **元素**
```ruby
arr = [1, 2, 3, 4, 5, 6]
arr[2]             #=> 3
arr[100]           #=> nil
arr[-3]            #=> 4
arr[2, 3]          #=> [3, 4, 5]
arr[1..4]          #=> [2, 3, 4, 5]
arr[1..-3]         #=> [2, 3, 4]
arr.at(0)          #=> 1
arr[1...-1]        #=> [2, 3, 4, 5]  
```
---
##**Array** pack 指令
- array to sring

```ruby
a = [ "a", "b", "c" ]
n = [ 65, 66, 67 ]
puts a.pack("A3A3A3")   #=> "a  b  c  "
puts a.pack("a3a3a3")   #=> "a0000b0000c0000"
puts n.pack("ccc")      #=> 数字转字符

```
---

##**Array** 迭代
```ruby
arr = [a,b,c]
arr.each { |x| print x}          #=> abc
arr.reverse_each { |x| print x}  #=> cba
```
---

### **Array** Map-Reduce 

```ruby
# map
a = [ "a", "b", "c", "d" ]
a.collect { |x| x + "!" }        #=> ["a!", "b!", "c!", "d!"]
a.map.with_index{ |x, i| x * i } #=> ["", "b", "cc", "ddd"]
a                                #=> ["a", "b", "c", "d"]

# reduce

# Sum some numbers
(5..10).reduce(:+)                             #=> 45
# Same using a block and inject
(5..10).inject { |sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                          #=> 151200
# Same using a block
(5..10).inject(1) { |product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest                                        #=> "sheep"
```
---

### Array\#**filter 过滤**

```ruby
[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]

a = %w{ a b c d e f }
a.select { |v| v =~ /[aeiou]/ }            #=> ["a", "e"]
```
---

### Array as **Stack**
- pop

```ruby
a = [ "a", "b", "c", "d" ]
a.pop     #=> "d"
a.pop(2)  #=> ["b", "c"]
a         #=> ["a"]
```
- push

```ruby
a = [ "a", "b", "c" ]
a.push("d", "e", "f")
        #=> ["a", "b", "c", "d", "e", "f"]
[1, 2, 3,].push(4).push(5)
        #=> [1, 2, 3, 4, 5]
```

---

## quiz

- 21点实现


<aside class="notes">
def black_jack cards
  x = cards.select { |x| x!="A" }.reduce(0) do |a, s|
    if "JQK".include? s
      a+10
    else
      a+s.to_i
    end
  end

  count = cards.count("A")

  if x+count <= 11
    x+count+10
  elsif x+count
  end
end

</aside>