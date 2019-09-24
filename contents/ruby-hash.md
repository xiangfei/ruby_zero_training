# ruby **Hash**

---


#**Hash** 说明
- 哈希（Hash）是类似 "employee" => "salary" 这样的键值对的集合
- 哈希的索引是通过任何对象类型的任意键来完成的, 其他与数组相似
---

##**Hash** 创建
```ruby
grades = { "Jane Doe" => 10, "Jim Doe" => 6 }
options = { :font_size => 10, :font_family => "Arial" }
grades = Hash.new
grades["Dorothy Doe"] = 9
```
---

##**Hash** 迭代

```ruby
books = {
    :matz => "The Ruby Language",
    :black => "The Well-Grounded Rubyist"
}
books.each { |author, name| puts "#{author}: #{name}" }
```

---
#### Keyword **Arguments** With Hashes
```ruby
class Person
  attr_accessor :first, :last, :weight, :height

  def initialize(params = {})
    @first = params[:first]
    @last = params[:last]
    @weight = params[:weight]
    @height = params[:height]
  end
end

p = Person.new(
    height: "170cm",
    weight: 72,
    last: 'Doe',
    first: 'John'
)
```
---

#### Keyword **Arguments**
```ruby
def foo(str: "foo", num: 424242)
  [str, num]
end

foo(str: 'buz', num: 9) #=> ['buz', 9]
foo(str: 'bar')         # => ['bar', 424242]
foo                     # => ['foo', 424242]
foo(bar: 'buz')         # => ArgumentError
```
- __Only after Ruby 2.0__

- http://brainspec.com/blog/2012/10/08/keyword-arguments-ruby-2-0/

