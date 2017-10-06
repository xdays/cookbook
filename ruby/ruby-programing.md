# variable

## scop

```
$x = 0
x = 0

require "./sub"

p $x   #=> 1
p x    #=> 0 
``

sub.rb

```
$x = 1  ## 对全局变量赋值
x = 1   ## 对局部变量赋值 
```

## asignment

``
a, b, c, d = 1, 2
a, b, c, d = 1, 2
a, b, * c = 1, 2, 3, 4, 5
a, * b, c = 1, 2, 3, 4, 5
```

# condition control

```
a = 10
b = 20
if a > b
  puts "a 比b 大"
elsif a < b
  puts "a 比b 小"
else
  puts "a 与b 相等"
end 
```

```
a = 10
b = 20
unless a > b
  puts "a 不比b 大"
en 
```

```
tags = [ "A", "IMG", "PRE" ]
tags.each do |tagname|
  case tagname
  when "P","A","I","B","BLOCKQUOTE"
    puts "#{tagname} has child."
  when "IMG", "BR"
    puts "#{tagname} has no child."
  else
    puts "#{tagname} cannot be used."
  end
end 
```

# loop

```
5.times do |i|
  puts i
end
```

```
sum = 0
for i in 1..5
  sum = sum + i
end
puts sum 

names = ["awk", "Perl", "Python", "Ruby"]
for name in names
  puts name
end
```

```
sum = 0
i = 1
while i <= 5
  sum += i
  i += 1
end
puts sum
```

```
names = ["awk","Perl","Python","Ruby"]
names.each do |name|
  puts name
end 
```

```
loop do
  print "Ruby!"
end
```


```
puts "break 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    break
  end
  p [i,lang]
end

puts "next 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    next
  end
  p [i,lang]
end

puts "redo 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    redo
  end
  p [i,lang]
end
```

# method

```
def hello(name="Ruby")
  puts "Hello, #{name}."
end

hello("Ruby")
```

```
def foo(*args)
  args
end

p foo(1, 2, 3)    #=> [1, 2, 3] 
```

```
def meth(x: 0, y: 0, z: 0, **args)
  [x, y, z, args]
end

p meth(z: 4, y: 3, x: 2)        #=> [2, 3, 4, {}]
p meth(x: 2, z: 3, v: 4, w: 5)  #=> [2, 0, 3, {:v=>4, :w=>5}]
```

# class and module

```
class HelloWorld                   # class 关键字
  def initialize(myname = "Ruby")  # initialize 方法
    @name = myname # 初始化实例变量
  end

  def hello                        # 实例方法
    puts "Hello, world. I am       #{@name}."
  end
end

bob = HelloWorld.new("Bob")
alice = HelloWorld.new("Alice")
ruby = HelloWorld.new

bob.hello 
```

```
class HelloWorld
  attr_accessor :name
end 
```

```
class << HelloWorld
  def hello(name)
    puts "#{name} said hello."
  end
end

HelloWorld.hello("John")    #=> John said hello.

class HelloWorld
  class << self
    def hello(name)
      puts "#{name} said hello."
    end
  end
end 

def HelloWorld.hello(name)
  puts "#{name} said hello."
end

HelloWorld.hello("John")    #=> John said hello. 
```

```
class AccTest
  def pub
    puts "pub is a public method."
  end

  public :pub   # 把pub 方法设定为public（可省略）

  def priv
    puts "priv is a private method."
  end

  private :priv # 把priv 方法设定为private
end
```
