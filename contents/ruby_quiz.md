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

##  写一个ruby gem


<aside class="notes">

Gem::Specification.new do |s|  
  s.name        = 'crowdSystem'  
  s.version     = '1.0.0'  
  s.date        = '2016-09-18'  
  s.summary     = "crowdSystem!"  
  s.description = "crowdSys automated test application"  
  s.authors     = ["shench"]  
  s.email       = 'xxxxxxx@xxxnets.com'  
  s.files       = ["lib/crowdSystem.rb", "lib/crowdSysAction.rb","lib/crowdSysENV.rb","rake/Rakefile","rake/startTest.ini","rake/startTest.rb","testcase/testCase_checkList.txt"]  
  s.homepage    = 'http://172.17.2.44:9527/welcome/index'
  s.license     = 'MIT'  
end
 </aside>













