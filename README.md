[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Ruby Inheritance

## Objectives

By the end of this, developers should be able to:

- Diagram the Ruby method lookup chain.
- Write a class which inherits from another class.
- Write a mixin.	
- Describe reasons why inheritance and Mixins are desirable.

## Ruby Inheritance

Ruby will be our first example of linking different objects together in a hierarchy. This process is called "inheritance" and the result is what we mean when we say an object "inherits" behavior from another object.

Some objects can be classified in multiple ways. These multiple classifications often make sense as a hierarchy. For example, a `Dog` is a kind of `Pet`. It's also a kind of `Animal`. In Ruby, we can share code (data or behavior) between two classes using **inheritance**. Let's look at an example of inheritance. Note that a Ruby class can only inherit from one other class, so whether you name that class `Pet` or `Animal` will depend on your application.

```ruby
class Animal
  def eat
    puts "Nom nom nom"
  end
end

class Dog < Animal
  def speak
    puts "woof"
  end
end

class Cat < Animal
  def speak
    puts "meow"
  end
end

dog = Dog.new
dog.eat # "Nom nom nom"
dog.speak # "woof"

cat = Cat.new
cat.eat # "Nom nom nom"
cat.speak # "meow"
```

### Lab: Inheritance

- Create a class named `Vehicle` which has a method named `start` that `puts "Engine is on!`.
- Create a class named `SpaceShip` which inherits from `Vehicle` and has a method named `fly` which puts `Up up and away!`.
- Create a class named `Car` which inherits from `Vehicle` and has a method named `drive` which puts `Vroom!`.

## Ruby: Super Inheritance

`Super` will call the same method defined in the `parent` or `superclass` and give you the result.

```ruby
class Animal
  def move
    "I can move"
  end
end

class Bird < Animal
  def move
    puts super + " by flying"
  end
end

class Fish < Animal
  def move
    puts super + " by swimming"
  end
end

bird = Bird.new
bird.move

fish = Fish.new
fish.move
```

### Lab: Super Inheritance

- Add a method named `move` to your `Vehicle` class that returns `Here we go `.
- Rename your `fly` method in your `SpaceShip` to `move` and use `super` so that it prints `Here we go Up up and away!`.
- Rename your `drive` method in your `Car` to `move` and use `super` so that it prints `Here we go Vroom!`.


## Mixins

Mixins are useful when we want to make chunks of code that are reusable across multiple classes but they do not inherit from the same class.  These "chunks" are called `modules`. Take a look at the code below:

```rb
# define module Sleeper
module Sleepable
  def go_to_sleep
    puts "nap time"
  end
end

# define Class Person
class Person
  include Sleepable
end

# define Class Computer
class Computer
  include Sleepable
end

dell = Computer.new
dell.go_to_sleep # "nap time"

human = Person.new
human.go_to_sleep # "nap time"
```

In the code above, we defined a `module` called Sleepable. We also define a `Person` class and a `Computer` class. By using the keyword `include` followed by the name of the module (in this case `Sleepable`) we have access to the methods we defined in our module.  This is great because it allows us to keep our code *D-R-Y*, not to mention it allows us to be lazy developers (the good kind of lazy).


```ruby
# define module Sleeper
module Sleepable
    def go_to_sleep(name)
      puts name + " wants power nap"
    end
  end
  
  # define Class Person
  class Person
    include Sleepable
  end
  
  # define Class Computer
  class Computer
    include Sleepable
  end
  
  dell = Computer.new
  dell.go_to_sleep("hp") # "nap time"
  
  human = Person.new
  human.go_to_sleep("saad") # "nap time"
```

-----------
### Labs
------------

### Lab: 1. Drawing the Method Lookup Chain in Ruby

Please diagram the method lookup chain using the following requirements:

- Create a class `TVShow` that has an instance method called `roll_credits`.
- Create a class `FamilyFeud` that inherits from the class `TVShow` and has an instance method called `fast_money`.
- Diagram creating a new instance of the `FamilyFeud`
- Diagram how Ruby finds and executes the methods called on  `FamilyFeud`

```rb
steve_harvey_family_feud = FamilyFeud.new
steve_harvey_family_feud.fast_money
steve_harvey_family_feud.roll_credits
```

------------

### Lab: 2. Model Shapes Using Classes

A `Rectangle` is a `Shape`, and a `Square` is a `Rectangle`.

#### Creating a 'Shape' Class

Define a Shape class with the following:
- `num_sides`: set during instantiation, read-only.
- `side_length`: set during instantiation, readable and writable.
- `color`: NOT set during instantiation, readable and writable.
- `Shape.new(num_sides, side_length)` should create a shape.
- `calculate_area` methodwhich calculates the area of a 'regular' shape (all sides equal) for the given side length. The mathematical formula for this is:
```
area = num_sides * length * length / (4 * tangent(PI/num_sides))
```

#### Creating a Rectangle Class

- Rectangles should be instantiated with `Rectangle.new(3, 4)` to create a rectangle with a length of 3 and a width of 4.
- Instances of Rectangle should respond to the `#calculate_area` method and give the correct result.

#### Creating a Square Class

- Squares should be instantiated with `Square.new(4)` to create a square with all sides equal to 4.
- Instances of Square should respond to the `#calculate_area` method and give the correct result.


 ------------


### Lab: 3. More on Inheritance

1. Create a class called `Dessert` that has instance variables of `@name` and `@sugar_content`
2. Give it an instance method of `eat` that puts `"Yum! This #{name} is sooooo delicious!"`
3. Make two new classes called `Pie` and `DeepFriedDessert` that inherit from `Dessert`
4. Give the `DeepFriedDessert` its own `eat` method that instead puts `"Yum! This #{name} is sooo...ack! ugh! *heart-attack*"`
5. Make a new class `IceCream` that inherits from `Dessert` use `super` to get the instance variables of `@name` and `@sugar-content`. Also give `IceCream` its own unique instance variable of `@toppings`


------------


### Lab 4. The Universe

#### Reps with Classes

#### Universe Part One

What's in a Class? A class can contain any number of variables and any number of methods. That is, any number of things and any number of actions. Therefore, let's make a Universe simulator! ;)

1. Make a Class called `Universe`.

2. Universe takes three parameters, `item1`, `item2`, `item3`: these are the three things within this universe we are making-- they could be anything: suns, galaxies, dust, people, lossless mp3s, justice,  temporal lobes, etc. Save these things into an array called `@items`.

3. Give the initialize method an instance variable `@expanding = true`

4. Give the initialize method an instance variable `@conservation = true`

5. Give the initialize method an instance variable
`@crunched = false`

6. Make a method `see_all_things` that will print out all the items in this universe. Test it out.

7. Make a method called `create` that takes a parameter `new_item` and will add the new item to the universe (in the `@items` array). If `@conservation = true` then one random item in the universe is *replaced* by the new thing. If not, then a new thing is added to the `@items` array.


#### Universe Part Two

8. While `@conservation` is true, run the `create` method to add a "mosquito" to your universe. Keep running it until all of the items in your universe are mosquitoes (they should be randomly replaced). You now have a mosquito universe. :(

9. Time to make a parallel universe. Make a new instance of your universe called `parallel`, and put three new things into it.

10. Make a method `check_density` that changes `expanding` to `false` if there are more than ten things in the universe (more than ten items in the `@items` array). This will mean that the universe is now contracting under its own gravity . . .  there's no stable universe in this scenario. We'll come back to this in a minute . . .

11. Make a method called `energy_conservation` that changes `conservation` from `true` to `false` if all items in the `@items` array are identical. Hint: check out the `.uniq` method.



#### Universe Part Three

12. Make a method called `crunch?` wherein, if `expanding` equals `false`, goes through each item in the `@items` array, sets it to `nil` and prints a string saying the name of the item and that it has been crunched due to gravity. When the entire contents of the array are `nil`, set the array itself to `nil` and print "The Universe has ended." If the universe has ended, set `@crunched` to `true`

13. Write your Universal Simulator that runs the following steps in a loop until the Universe has ended. The Universe has ended when `@crunched` is `true`. You might want to make `@crunched` available with `attr_accessor`. Start by making a new instance of the Universe.

	* print the contents of `@items`
	* add an item to `@items`
	* check conservation
	* check density
	* crunch?

Possible output:
```
spam
github
lava
spam has been crunched due to gravity
github has been crunched due to gravity
lava has been crunched due to gravity
radio waves has been crunched due to gravity
The Universe has ended
=> true

```

----------

## Additional Resources

- http://www.zenruby.info/2016/06/ruby-classes.html
- https://www.codequizzes.com/ruby/intermediate/inheritance-ancestors-super
- https://www.codequizzes.com/ruby/intermediate/monkey-patching-modules-singleton-methods
