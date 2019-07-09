---
layout: post
title:      "What is self?"
date:       2019-07-09 08:59:10 +0000
permalink:  what_is_self
---


Similar to a person having multiple facets to their personality, and depending on the circumstance or situation depends on how and which facet is shown in that circumstance or situation, `self` allows us to call on itself in various ways dependent on the context in which the `self` keyword is used within our code.

When `self` is called outside of a block of code, it will be identified as the global object itself, for example:
puts "Self's class is #{self.class}."```

outputs:
Self's class is Object.```

`self` when called inside of a class defines the class name as the class.
```class Horoscope
   puts "Self is #{self}."
end```

outputs:
```Self is Horoscope.```

We could also replace `self` with `Horoscope` here and our output would remain the same as they are interchangeable when called within a class.
```class Horoscope
  puts "Self is #{Horoscope}."
end```

outputs:
```Self is Horoscope.```

Going a step further, if we define a class variable within our class, we can then call that class variable within a method that calls on itself.
```
class Horoscope
    @@sign = "Aquarius"
 
    def self.name
        puts "Self inside class method is: #{self}."
        return @@sign
    end
end
 
puts "Horoscope class method name is: #{Horoscope.name}."
```

outputs:
```
Self inside class method is: Horoscope.
Horoscope class method name is: Aquarius.
```

_Note we must explicitly return our class variable `@@sign` within our `self.name` method, otherwise when we try to interpolate and call `Horoscope.name` outside of the class, nothing will print to the screen as we have not set a return value for the method._

Lastly, we can define self as an instance of a class method, however in order to obtain any information from it we will need to create a new instance of the class.
 
```
class Horoscope
 
    def sign
        puts "Self inside the instance method is: #{self}."
        puts "Self.class inside the instance method is #{self.class}."
        return "Aquarius"
    end
end

horoscope = Horoscope.new
puts "Horoscope instance method 'sign' is: #{horoscope.sign}."
```

outputs:
```
Self inside the instance method is: #<Horoscope:0x00005599135f5e40>.
Self.class inside the instance method is Horoscope.
Horoscope instance method 'sign' is: Aquarius.
```

Here `#{self}` displays the object that was instantiated when we called `.new` on the `Horoscope` class.  `#{self.class}` tells us the name of the parent class in which self was called from.  `#{horoscope.sign}` outputs the value we set when setting the return value to “Aquarius” within the sign method.
