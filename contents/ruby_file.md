# **Ruby** 文件


---

##  创建文件


```ruby
File.open("filename", "w+") do |aFile|
   
end
```

---

## 读文件

```ruby

File.open("filename", "r+") do |aFile|
   aFile.read
end

```
---

## 写文件

```ruby

File.open("filename", "w+") do |aFile|
   aFile.write "ads"
end

```

---

## rename

```

File.rename
```

---

## quiz 

- 读文件文件,查看字符串匹配







