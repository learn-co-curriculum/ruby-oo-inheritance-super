# Ruby Inheritance: Using the `super` Keyword

## Introduction

So far, we've seen the benefits of using inheritance to create a group of classes that share certain characteristics and behaviors. However, up until now, the implementation of shared characteristics has been somewhat rigid. If class `Student` inherits from class `User`, we can choose to either allow the `Student` class to inherit a certain method from `User` or overwrite that method with another implementation that is specific to `Student`. 

But what if there is a method in the parent class that we want our child to share *some* of the functionality of? Or what if we want our child class to inherit a method from the parent and then augment it in some way? We can achieve this with the use of the `super` keyword. 

## Using `super` to supercharge inheritance

Let's say we are working on an education app in which users are either students or teachers. We have a parent, `User` class, that both our `Student` and `Teacher` classes inherit from. 

Our `User` class has a method, `log_in`, that sets an instance variable, `@logged_in` equal to `true`. 

```ruby
class User

  def log_in
    @logged_in = true
  end
end
```

However, when a student logs into our app, we need to not only set their logged in attribute to `true`, we need to set their "in class" attribute to true. We could simply edit the `#log_in` method in the `User` class to account for this. But that doesn't make sense here. Remember that both `Student` and `Teacher` inherit from `User`. Teachers don't need to indicate that they are "in class", so we don't want to alter the `#log_in` method of our parent class and inadvertently give teachers some behavior that they don't want or need. 

Instead, we can augment, or supercharge, the `#log_in` method *inside* of the `Student` class. 

Let's take a look:

```ruby
class Student < User
  def log_in
    super
    @in_class = true
  end
end
``` 

Here, we re-define the `#log_in` method and tell it to inherit any functionality of the `#log_in` method defined in the parent, or "super", class, which is `User`. 

In the `#log_in` method above, the `super` keyword will call on the `#log_in` method as defined in the super class. *Then*, the additional code that we're adding into our `Student#log_in` method will also run. We have therefore supercharged our `#log_in` method, for the `Student` class only. 
