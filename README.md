# Week Seven Homework

## A new method for making methods
The usual way of defining new methods is to put your intended logic between def & end. And that works perfectly fine for the most part.
But consider a situation where you have to create a series of methods all of which have the same basic structure save for one string, and which can only be one of a certain set of strings. Now, you might say we'll just define one method and accept that one string as a parameter, which we can then use wherever we want. And you'd be right. But, the problem with such an approach is it's not particularly declarative: you don't know exactly what values that optional parameter can accept.

```ruby
class Doctor

define_method("perform_rhinoplasty") do |argument|
"performing rhinoplasty on #{argument}"
end

define_method("perform_checkup") do |argument|
"performing checkup on #{argument}"
end

define_method("perform_interpretive_dance") do |argument|
"performing interpretive dance on #{argument}"
end
end

doctor = Doctor.new
puts doctor.perform_rhinoplasty("nose")
puts doctor.perform_checkup("throat")
puts doctor.perform_interpretive_dance("in da club")
```

The above piece of code causes three methods perform_rhinoplasty, perform_checkup, andperform_interpretive_dance to be created. And invoking them calls the respective blocks that were passed to the define_method call. This is clearly no better than just defining methods the old-fashioned way. In fact, it's a little bit worse since we've just added a bunch of extra words and strings and gained nothing for it.

## Real Ultimate Power
The real power of define_method is realised when we realise we call it like any other code. Here's an example where we call it inside a loop and it achieves the same result as above.
Example Code:

```ruby
class Doctor
  ["rhinoplasty", "checkup", "interpretive_dance"].each do |action|
    define_method("perform_#{action}") do |argument|
      "performing #{action.gsub('_', ' ')} on #{argument}"
    end
  end
end
 
doctor = Doctor.new
puts doctor.perform_rhinoplasty("nose")
puts doctor.perform_checkup("throat")
puts doctor.perform_interpretive_dance("in da club")
```
 
Isn't that nice? We have code that's generating the code for us. Pretty meta, isn't it?
In fact, we can now extend this by adding any number of elements to that array -- or replacing the array entirely with an external data source. Many Ruby libraries use exactly this technique to define methods dynamically based on, say, database schemas. Rails, for example, will create methods such as Customer#find_by_first_name_and_last_name.

## Do you have the Real Ultimate Power?
Create a class Monk which can meditate on life, the universe or everything. It should have three methods meditate_on_life, meditate_on_the_universe & meditate_on_everything and returns strings of "I know the meaning of life", "I know the meaning of the universe", and "I know the meaning of everything", respectively.
