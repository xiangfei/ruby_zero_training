# **Ruby** quiz


---

##  判断数组维度

<aside class="notes"> 
def dimension(array)
  return 0 if array.class != Array || array.empty?
  max = 0
  array.each do |a|
    t = dimension(a)
    max = [max, t].max
  end
  max + 1
end

p dimension([[[1,2],[2,[3,[4]]]],[[3,4],[5]]])

</aside>

---

## 创建


```ruby
Thread.new 

```


---

## 多线程











