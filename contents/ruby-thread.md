# **Ruby** 多线程


---
## 多线程
- 每个正在系统上运行的程序都是一个进程。每个进程包含一到多个线程。
- 线程是程序中一个单一的顺序控制流程，在单个程序中同时运行多个线程完成不同的工作,称为多线程。
- Ruby 中我们可以通过 Thread 类来创建多线程，Ruby的线程是一个轻量级的，可以以高效的方式来实现并行的代码。
--- 
## 创建 Ruby 线程
- 要启动一个新的线程，只需要调用 Thread.new 即可


```ruby

t = Thread.new {
  sleep 10
}
t.join
puts 12
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
#sleep 10
12
    </code>
  </pre>

</div>

---

## 线程描述

- 线程的创建Thread.new,Thread.start,Thread.fork这三个方法来创建线程。
- 创建线程后无需启动,线程会自动执行.
- Thread 类定义了一些方法来操控线程.线程执行Thread.new中的代码块。
- 线程代码块中最后一个语句是线程的值,可以通过线程的方法来调用，如果线程执行完毕，则返回线程值，否则不返回值直到线程执行完毕.
- Thread.current 方法返回表示当前线程的对象.Thread.main 方法返回主线程。
- 通过 Thread.Join 方法来执行线程,这个方法会挂起主线程

---

## 线程状态

线程有5种状态：

线程状态  |返回值
:--: | :--:
Runnable  |run
Sleeping  |Sleeping
Aborting  |aborting
Terminated normally |false
Terminated with exception |nil

---

## 线程和异常

- 当某线程发生异常，且没有被rescue捕捉到时，该线程通常会被无警告地终止
- 若有其它线程因为Thread#join的关系一直等待该线程的话，则等待的线程同样会被引发相同的异常

```ruby
begin
  t = Thread.new do
    Thread.pass    # 主线程确实在等join
    raise "unhandled exception"
  end
  t.join
rescue
  p $!  # => "unhandled exception"
end
```

--- 

## 异常终止
 - Thread.abort_on_exception
  - 默认false 
  - 设置true thread 异常 解释器也会异常终止 

```bin
2.4.2 :003 > Thread.abort_on_exception = true
 => true 
2.4.2 :004 > t = Thread.new do
2.4.2 :005 >     sleep 10
2.4.2 :006?>   raise
2.4.2 :007?>   end
 => #<Thread:0x00007f2b48e54a28@(irb):4 sleep> 
2.4.2 :008 > (irb):6:in `block in irb_binding': unhandled exception
[root@autotest-ruby-agent automationtesting-backend]# 
```




---

## 线程同步控制
- 通过Mutex类实现线程同步
- 监管数据交接的Queue类实现线程同步
- 使用ConditionVariable实现同步控制

---


## 通过Mutex类实现线程同步

- 如果在多个线程钟同时需要一个程序变量，可以将这个变量部分使用lock锁定

```ruby
require "thread"
puts "Synchronize Thread"

@num=200
@mutex=Mutex.new

def buyTicket(num)
   @mutex.lock
       if @num>=num
           @num=@num-num
         puts "you have successfully bought #{num} tickets"
      else
          puts "sorry,no enough tickets"
      end
   @mutex.unlock
end

ticket1=Thread.new 10 do
    10.times do |value|
   ticketNum=15
  buyTicket(ticketNum)
  sleep 0.01
    end
end

ticket2=Thread.new 10 do
  10.times do |value|
   ticketNum=20
  buyTicket(ticketNum)
  sleep 0.01
    end
end

sleep 1
ticket1.join
ticket2.join

```

---

## 监管数据交接的Queue类实现线程同步

<aside class="notes" >
  Queue类就是表示一个支持线程的队列，能够同步对队列末尾进行访问。不同的线程可以使用统一个对类，但是不用担心这个队列中的数据是否能够同步，另外使用SizedQueue类能够限制队列的长度

SizedQueue类能够非常便捷的帮助我们开发线程同步的应用程序，应为只要加入到这个队列中，就不用关心线程的同步问题。

</aside>


```ruby
require "thread"
puts "SizedQuee Test"

queue = Queue.new

producer = Thread.new do
     10.times do |i|
          sleep rand(i) # 让线程睡眠一段时间
          queue << i
          puts "#{i} produced"
     end
end

consumer = Thread.new do
     10.times do |i|
          value = queue.pop
          sleep rand(i/2)
          puts "consumed #{value}"
     end
end

consumer.join

```




---

## 使用ConditionVariable实现同步控制

```ruby
mutex = Mutex.new
resource = ConditionVariable.new

waiting_thread = Thread.new {
  mutex.synchronize {
    puts "Thread 'a' now needs the resource"
    resource.wait(mutex)
    puts "'a' can now have the resource"
    "a can now have the resource"
  }
}

signal_thread = Thread.new {
  mutex.synchronize {
    puts "Thread 'b' has finished using the resource"
    resource.signal
  }
}
```



Thread 'a' now needs the resource
Thread 'b' has finished using the resource
'a' can now have the resource

---

## 线程互斥

- 是一种用于多线程编程中，防止两条线程同时对同一公共资源（比如全局变量）进行读写的机制。

```ruby
require 'thread'

count1 = count2 = 0
difference = 0
counter = Thread.new do
   loop do
      count1 += 1
      count2 += 1
   end
end
spy = Thread.new do
   loop do
      difference += (count1 - count2).abs
   end
end
sleep 1
puts "count1 :  #{count1}"
puts "count2 :  #{count2}"
puts "difference : #{difference}"

```


<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
count1 :  9712487
count2 :  12501239
difference : 0
    </code>
  </pre>

</div>

---

## 线程互斥

- mutex

```ruby
#!/usr/bin/ruby
require 'thread'
mutex = Mutex.new

count1 = count2 = 0
difference = 0
counter = Thread.new do
   loop do
      mutex.synchronize do
         count1 += 1
         count2 += 1
      end
    end
end
spy = Thread.new do
   loop do
       mutex.synchronize do
          difference += (count1 - count2).abs
       end
   end
end
sleep 1
mutex.lock
puts "count1 :  #{count1}"
puts "count2 :  #{count2}"
puts "difference : #{difference}"

```

---

## 死锁

- 两个以上的运算单元，双方都在等待对方停止运行，以获取系统资源，但是没有一方提前退出时，这种状况，就称为死

<aside class="notes">
  
  Thread::stop → nil

Stops execution of the current thread, putting it into a “sleep” state, and schedules execution of another thread.

Thread#join → thr
Thread#join(limit) → thr

The calling thread will suspend execution and run thr. Does not return until thr exits or until limit seconds have passed. If the time limit expires, nil will be returned, otherwise thr is returned.
</aside>
```ruby
#!/usr/bin/ruby
require 'thread'
t = Thread.new { Thread.stop }
t.join 

```


<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
Traceback (most recent call last):
        5: from /usr/local/rvm/rubies/ruby-2.6.3/bin/irb:23:in `<main>'
        4: from /usr/local/rvm/rubies/ruby-2.6.3/bin/irb:23:in `load'
        3: from /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/gems/2.6.0/gems/irb-1.0.0/exe/irb:11:in `<top (required)>'
        2: from (irb):3
        1: from (irb):3:in `join'
fatal (No live threads left. Deadlock?)
2 threads, 2 sleeps current:0x0000000001c74470 main thread:0x0000000001c74470
* #<Thread:0x0000000001ca3388 sleep_forever>
   rb_thread_t:0x0000000001c74470 native:0x00007fb8eadd2740 int:0
   (irb):3:in `join'
   (irb):3:in `irb_binding'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb/workspace.rb:85:in `eval'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb/workspace.rb:85:in `evaluate'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb/context.rb:385:in `evaluate'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb.rb:493:in `block (2 levels) in eval_input'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb.rb:647:in `signal_status'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb.rb:490:in `block in eval_input'
   /usr/local/rvm/rubies/ruby-2.6.3/lib/ruby/2.6.0/irb/ruby-lex.rb:246:in `block (2 levels) in each_top_level_statement'
    </code>
  </pre>

</div>

