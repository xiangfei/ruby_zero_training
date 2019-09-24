# **Ruby** 简介


---

## Ruby 的特性
- Ruby 是开源的，在 Web 上免费提供，但需要一个许可证。
- Ruby 是一种通用的、解释的编程语言。
- Ruby 是一种真正的面向对象编程语言。
- Ruby 是一种类似于 Python 和 Perl 的服务器端脚本语言。
 - 这个语言最大的特点就是__对程序员友好__,而不是 __编译器友好__
- 代码少,效率高.
- Ruby 语法简单，这使得新的开发人员能够快速轻松地学习 Ruby。
- Ruby 可扩展性强，用 Ruby 编写的大程序易于维护。
- Ruby 可以安装在 Windows 和 POSIX 环境中

---
## Ruby能用来干什么
- Ruby 可以用来编写通用网关接口（CGI）脚本。
- Ruby 可以被嵌入到超文本标记语言（HTML）。
- Ruby 与 C++ 和 Perl 等许多编程语言有着类似的语法。
- Ruby 可用于开发的 Internet 和 Intranet 应用程序。
- Ruby 支持许多 GUI 工具，比如 Tcl/Tk、GTK 和 OpenGL。
- Ruby 可以很容易地连接到 DB2、MySQL、Oracle 和 Sybase。
- Ruby 有丰富的内置函数，可以直接在 Ruby 脚本中使用。

---


## Ruby Java 比较

- 各种括号 (), {}
- 行末的分号是.
- 参数前面的 *.
- 写一段实现代码(implement)之前,必须要先写接口(interface)
- 一个方法,前面必须有 两个前缀?( public void method() {} )

<div class="fragment fade-in-then-out"><div style="color:red">ruby 都不需要</div></div>

---

## 为什么要学ruby
- 让你的工作更加快乐.
- Ruby程序员平均工资最高. 为什么? 因为一个Ruby程序员干的活儿, 顶的上3~5个其他语言的程序员.

--- 
## Ruby不关心变量是什么类型
- 所以，这让我们非常省心。你不需要在调用一个变量之前,还要考虑它的类型. 就好比我们在写一段循环代码的时候, 需要去考虑汇编语言的寄存器吗?

```ruby

name = "Jim" # string
six = 6 # int
fruits = ['apple', 'banana']  #array
```

---

## 极其简单
如果你接触过C/C++, java, object C等语言，回过头再看Ruby，就会发现它特别简洁，代码极度好懂．

ruby: 一行代码:
```ruby
puts "hello, world!"
```
c/java:
```java
package 'x.y';

public 
```
---
## Ruby是让人快乐的
- 使用c, java的时候，你会发现世界很昏暗。做一件很小的事情都要费很大的力气。
- 使用了ruby之后，时间多了，爱好多了，有时间找女朋友了。
- 大部分Ruby程序员都是全栈工程师,因为我们工作轻松, 可以学习的时间多.
---

## Ruby最省心
- java程序员不关心指针.
- Ruby程序员不关心变量类型.
- 所以，我们可以把心思都放在业务逻辑上。
- 所以，Ruby程序员是快乐的。

---
## 生产率极高
- 一个Ruby程序员顶3个其他程序员.
 - 其他程序员包括: c, java, .net, php.
- 所以硅谷创业公司绝大部分都选择Ruby作为开发语言.

---

## 安装Ruby
虽然系统默认自带了Ruby，但是不如我们自定义的灵活．
我们使用rbenv 来安装Ruby,　最大的好处是 可以允许你同时安装多个Ruby版本．

--- 
## 什么是rbenv
- rbenv(ruby environment),是管理多个不同版本的ruby工具，是之前rvm(ruby version manager)的替代品。
类似的工具还有管理不同Node版本的nvm(node version manager)。
---
## 安装步骤

```bash
git clone git://github.com/rbenv/rbenv.git ~/.rbenv 
export  PATH=$HOME/.rbenv/bin:$PATH
rbenv install --list  #查看版本 
rbenv install 2.2.1 #安装
rbenv global 2.1.2 #全局ruby
```

---
## irb
- 交互式ruby 
- 命令行解析器 


```shell
$ irb
irb(main):001:0> puts "Hello, World"
Hello, World
=> nil
irb(main):002:0> 1+2
=> 3

```


---

## RubyGems

- 包管理工具
- 基础命令
  * `$ gem search rspec`
  * `$ gem install rspec`
  * `$ gem list`
  * `$ gem list rspec -d`
  * `$ gem uninstall rspec`
  * `$ gem environment gemdir`

---

## Gem是什么

- 有一下组件构成:
  * 代码
  * gemspec 文件

- 下面是一个标准的gem:

```bash
% tree freewill
freewill/
├── bin/
│   └── freewill
├── lib/
│   └── freewill.rb
├── test/
│   └── freewill_spec.rb
├── README
├── Rakefile
└── freewill.gemspec
```

---

## Rake

- ruby的make实现,类似ant,maven ,gradle
- 标准的ruby语法
- 1.9 以后ruby的标准库

---

## rake command

- 在Rakefile文件下运行
- rake
  - 运行Rakefile的默认task
- $ rake -T
  - 查看rake task

---

### Rakefile
<!-- <div style="position: absolute; width: 40%; right: 10%; box-shadow: 0 1px 4px rgba(0,0,0,0.5), 0 5px 25px rgba(0,0,0,0.2); background-color: rgba(0, 0, 0, 0.9); color: #fff; padding: 20px; font-size: 20px; text-align: left;">   
  <p>
    Since reveal.js runs on the web, you can easily embed other web content. Try interacting with the page in the background.
  </p>
</div> -->
<aside class="notes">
    Oh hey, these are some notes. They'll be hidden in your presentation, but you can see them if you open the speaker notes window (hit 's' on your keyboard).
</aside>

```ruby
# Simple Tasks


task :name

# Tasks 依赖
task :name => [:prereq1, :prereq2]

# Simple Example

task :default => [:test]

task :test do
  puts "Hello World!"
end

# Tasks with Arguments

task :name, [:first_name, :last_name] do |t, args|
  args.with_defaults(:first_name => "Xi", :last_name => "Qi")
  puts "First name is #{args.first_name}"
  puts "Last  name is #{args.last_name}"
end
# Have Prerequisites

task :name, [:first_name, :last_name] => [:pre_name]

# comments
desc "Print 'Hello world!'"
task :hello do
	puts "Hello world!"
end

# Namespaces
namespace "main" do
  task :build do
    puts "main build"
  end
end

```


---


## Bundler

- 管理 gem

```bash
$ gem install bundler
$ bundle init

$ bundle install
```

---

## Gemfile

```ruby
source 'https://rubygems.org'

gem 'awesome_print'
gem 'rails', '3.0.0.beta3'
gem 'rack', '>=1.0'
gem 'thin', '~>1.1'
# gem 'thin', '>= 1.1', '< 1.2'

gem 'sinatra', :require => 'sinatra/base'
gem 'capybare-webkit', :require => false
```

---
### Bundler.require

```ruby
require 'bundler/setup'
Bundler.require(:default)

ap "Hello World!"
```

---

### Groups

```ruby
gem 'wirble', :group => :development
gem 'debugger', :group => [:development, :test]

group :test do
  gem 'rspec'
end
```

```bash
$ bundle install --without=development test
```

---

## Gemfile.lock
- bundle install 成功会产生
---

## bundle exec
```bash
$ bundle exec rspec
```

---


## RSpec

- 一个测试工具
- a rich command line program (the rspec command)
- textual descriptions of examples and groups (rspec-core)
- flexible and customizable reporting
- extensible expectation language (rspec-expectations)
- built-in mocking/stubbing framework (rspec-mocks)

---

bowling_spec.rb

```ruby
require 'bowling'

describe Bowling, "#score" do
  it "returns 0 for all gutter game" do
    bowling = Bowling.new
    20.times { bowling.hit(0) }
    expect(bowling.score).to be(0)
  end
end
```

---

bowling.rb
```ruby
class Bowling
  def hit(pins)
  end

  def score
    0
  end
end
```

```bash
$ rspec bowling_spec.rb
```

---

# **酷炫的东西!**

---

## __任意大__的整数

    2**10000 # ....
```ruby
1996168403619459789933112942320912427155649134941378111759378593209632395785573004679379452676
5246551266059895520550086918193311542508608460618104685509074866089624888090489894838009253941
6332578506215683094739025569123880652250966438744410467598716269854532228685381616943157756296
4076283688076073222853509164147618395638145896946389941084096053626782106462142733339403652556
5649530603142680234969400335934316651459297773279665775606172582031407994198179607378245683762
2800373028854872519008344645814546505579296014148339216157345881392570953797691192778008269577
3567444412306201875783632550272832378927071037380286639303142813324140162419567169057406141965
4342324638801248856147305207431992259611796250130992860241708340807605932320161268492288496255
8413128440615367389514871142563151110897455142033138202029316409575964647560104058458415660720
4496286701651506192063100418642227590867090057460641785695191145605506825125040600751984226189
......
......
......
```

    (2**10000).to_s.length # => 3011
    (2..10000).class  # => Bignum < Integer
---
## __并行__赋值
```ruby
x, y, z = 1, 2, 3 # => x=1 y=2 z=3

x, y = 1, 2, 3 # => x=1 y=2 z=nil

x = 1, 2, 3   # => x = [1, 2, 3]

x, *y, z = 1, 2, 3, 4 # => x=1, y=[2, 3], z=4

x, y, z = 1, *[2, 3]  # => x=1 y=2 z=3

a, (b, (c, d)) = [1, [2, [3, 4]]]

a, b = b, a  # => 交换 a, b
```
---

## splat(__*__) 参数
```ruby
def some_meth(*args)
  p args
end

some_meth(1, 2, 3, 4)   # => [1, 2, 3, 4]

args = [1, 2, 3, 4]
some_meth(*args)    # => [1, 2, 3, 4]
```

---
## 字符串的 __[]__ 方法
```ruby
str = "hello world!"

str[0]   # => 'h'
str[-1]   # => '!'
str[0..3] # => 'hell'
str[0...3] # => 'hel'
str[0, 4] # => 'hell'
str['!']  # => '!'
str[/he*\B/]  # => 'hello'
str[/(he)ll(o)/, 2] # => 'o'
```
---
## 强大的 __正则表达式__

```ruby
# 零宽断言
str = "red, white, and blue."
str.scan(/\w+(?=,)/)  # => ["red", "white"]

# 回文
"`abcba' is a palindromes".match(/(.)(.)(.)\k<-1>?\k<-2>\k<-3>/)
# => #<MatchData "abcba">

# 汉字
"one 汉字".match(/\p{han}+/)  # => '汉字'
```
---
## 神奇的 __==__ 方法
```ruby
require 'bcrypt'
include BCrypt

# create a Password instance.
password = Password.create('hello')

p password == 'hello'    # => true

p password
# => "$2a$10$qbDd3IegZotD7X828QFpauLCKy1ZcwT7bgXJfjTRSMLMU/J2gTSWi"

p password.class  # => BCrypt::Password < String

class Password < String
  def ==(secret)
    super(BCrypt::Engine.hash_secret(secret, @salt))
  end
end
```
---
## 神奇的 __===__ 方法 和 __case__ 语句

```ruby
class Range
  def ===(other)
    self.include? other.abs
  end
end

def meth(x)
  case x
  when 10..30  # (10..30) === x
    puts "in 10-30"
  else
    puts "not in 10-30"
  end
end

meth(15)  # => 'in 10-30'
meth(-15) # => 'in 10-30'
```
---
## 计算: 1m/4 + 10cm * 3 - 5mm
```ruby
# open class, 甚至 Fixnum (核心类) 也不例外.

class Fixnum
  def m; self*1000 end
  def cm; self*10 end
  def mm; self*1 end
end

1.m/4 + 10.cm * 3 - 5.mm  # => 545
```
---
## 内部__迭代器__
```ruby
  2.times { puts "hello world!" }  # =>
                                     hello world!
                                     hello world!
  [1, 2, 3, 4].map {|x| x * x } # => [1, 4, 9, 16]
  [1, 2, 3, 4].select {|x| x > 2 } # => [3, 4]
  (100..1000).step(100).to_a
  # => [100, 200, 300, 400, 500, 600, 700, 800, 900, 1000]
  (1..10).reduce(:+) # => 55
```
---
## Terminal 下__文本处理__
```sh
# 反转文件的每一行 (rev 命令)
cat 1.txt | ruby -lne 'puts $_.reverse'
# 将两个空行换为一个空行.
ruby -e 'STDIN.readlines.join.gsub(/\n\n/, "\n")' 1.txt
# 统计行数. (wc 命令)
ruby -e 'while gets; end; puts $.' 1.txt
# 打印文件前十行 (head 命令)
ruby -pe 'exit if $. > 10' 1.txt
# 打印匹配正则的行 (grep 命令)
ruby -ne 'print if /regex/' 1.txt
```


