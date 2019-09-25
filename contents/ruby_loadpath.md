# **Ruby** PATH路径


---

## 启动ruby 默认path

- 默认加载当前文件夹

```ruby
2.4.2 :003 > puts $LOAD_PATH
/usr/local/rvm/gems/ruby-2.4.2@global/gems/did_you_mean-1.1.0/lib
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0/x86_64-linux

```


---


## ruby 命令制定LOAD_PATH


```ruby
ruby -Iroot a.rb

[root@autotest-ruby-agent ~]# ruby -Iroot b.rb 
/root/root
/usr/local/rvm/gems/ruby-2.4.2@global/gems/did_you_mean-1.1.0/lib
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0/x86_64-linux


```

---
## 加载多个PATH

```
ruby -Iroot  -I/root b.rb 

/root/root
/root
/usr/local/rvm/gems/ruby-2.4.2@global/gems/did_you_mean-1.1.0/lib
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/site_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby/2.4.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/vendor_ruby
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0
/usr/local/rvm/rubies/ruby-2.4.2/lib/ruby/2.4.0/x86_64-linux


```