# **Ruby** Fiber


---
## Fiber

<aside  class="notes"> 
  不能做并发,做流程控制

Concurrency is when two tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. Eg. multitasking on a single-core machine. Parallelism is when tasks literally run at the same time, eg. on a multicore processor
</aside>

- Fibers是在Ruby中实现轻量级协同并发的原始语言。基本上，它们是创建可以暂停和恢复的代码块的手段，非常类似于线程。主要区别在于它们永远不会被抢占，调度必须由程序员而不是VM来完成
- 每个fiber都附带一个堆栈。这可以使fiber在fiber模块内从深度嵌套的函数调用中暂停
- fiber创建时不会自动运行


---

## demo

<aside  class="notes"> 


</aside>


```ruby

fiber = Fiber.new do
  Fiber.yield 1
  2
end

puts fiber.resume
puts fiber.resume
puts fiber.resume
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
1
2
FiberError: dead fiber called
    </code>
  </pre>

</div>

---

## fiber resume参数

- 如果第一次调用被当作块参数
- 不是 返回 调用 yield 方法的值

<aside class="notes">
  The Fiber#resume method accepts an arbitrary number of parameters, if it is the first call to resume then they will be passed as block arguments. Otherwise they will be the return value of the call to Fiber.yield

Example:

</aside>


```
fiber = Fiber.new do |first|
  second = Fiber.yield first + 2
end

puts fiber.resume 10
puts fiber.resume 14
puts fiber.resume 18

```
<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
12
14
FiberError: dead fiber called
    </code>
  </pre>

</div>