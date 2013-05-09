---
layout: post
title: A Ruby Scoping Gotcha?
categories: blog ruby code
---
Let's take this basic class:
``` ruby
class TestClass
  attr_accessor :one
  
  def my_method(branch=true)
    if branch
      puts "Do nothing to modify `one`"
    else
      puts "Modify `one` but it's a local variable"
      one = "test"
    end
    
    one # local variable
  end
  
  def my_non_modifying_method(branch=true)
    if branch
      puts "Do nothing to modify `one`"
    else
      puts "Do nothing to modify `one` either"
    end
    
    one #method call
  end
end
```

``` ruby
o = TestClass.new
o.one = "Value"

puts o.my_method 
 => nil #might expect 'Value' if you're not paying attention
puts o.my_non_modifying_method #expects "Value"
 => "Value"
puts o.my_method(false)
 => "test"
puts o.my_non_modifying_method(false) #expects "Value"
 => "Value"
```

So remember, if you create any local variables anywhere in your method, even if they're not called, they override the accessor methods and will give you results you're not expecting.  To get around it, make sure you always use self.<i>accessor</i>= to assign values when there is ambiguity.
