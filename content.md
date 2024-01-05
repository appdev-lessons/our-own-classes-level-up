# Our own classes: level up

## Initializers

When we create a new instance of a class, it's often necessary to initialize it with some data in order to be useful. This is where the `initialize` method comes in. This special method is called automatically when you create a new object. Let's see it in action.

Consider our Person class:

```ruby
class Person
  attr_accessor :first_name, :last_name, :role

  def initialize(first_name, last_name, role)
    @first_name = first_name
    @last_name = last_name
    @role = role
  end
end

person = Person.new("Ian", "Heraty", "Instructor")
pp person.first_name
pp person.last_name
pp person.role
```

{: .repl #person_initializer title="Person Initializer" points="1"}

The initialize method takes three parameters and assigns them to the instance variables. Now, when we create a new Person, we provide these details upfront, making our code cleaner and more intuitive.

## Setters and Getters
<!-- TODO: explain why a custom setter is useful (maybe use titleize in setter?) -->
<!-- TODO: explain better how attr_accessor method auto-creates setter/getter -->

In Ruby, setters and getters are methods that allow you to set and get the value of an object's attributes. We've already seen attr_accessor in action, which is a shorthand for both setter and getter methods. Let's break it down:

```ruby
class Person
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end

  # Getter for first_name
  def first_name
    @first_name
  end

  # Setter for first_name
  def first_name=(value)
    @first_name = value
  end

  # Similarly for last_name...
end

person = Person.new("Iannn", "Heraty")
pp person.first_name # Using getter
person.first_name = "Ian" # Using setter
pp person.first_name
```
{: .repl #person_setter_getter title="Person Setters and Getters" points="1"}

## Practice with Initializers and Setters/Getters
Let's put these concepts into practice. Define a Car class with the following requirements:

It should have make, model, and year attributes.
Use an initializer to set these attributes when a new Car object is created.
Also, create explicit setter and getter methods for these attributes.
Here's a skeleton to help you start:

```ruby
class Car
  # Your code here
end

# Test your Car class
car = Car.new("Toyota", "Camry", 2021)
pp car.make
pp car.model
pp car.year

# Change and then print the model
car.model = "Corolla"
pp car.model
```
{: .repl #car_class title="Car Class" points="1"}

```ruby
describe "Car class" do
  it "initializes with make, model, and year" do
    car = Car.new("Toyota", "Camry", 2021)
    expect(car.make).to eq("Toyota")
    expect(car.model).to eq("Camry")
    expect(car.year).to eq(2021)
  end

  it "allows changing the model" do
    car = Car.new("Toyota", "Camry", 2021)
    car.model = "Corolla"
    expect(car.model).to eq("Corolla")
  end
end
```
{: .repl-test #car_class_test for="car_class" title="Car Class Tests" points="1"}

## Summary
Understanding initializers and setters/getters is fundamental in Ruby, especially as you start building more complex applications. These concepts help encapsulate and manage data within your objects effectively.

Now, it's your turn to implement these concepts in the Car class. Once you're done, you'll be well on your way to mastering the basics of Ruby's object-oriented programming!

Remember: Test your code thoroughly and ensure it meets all the requirements!

When you are done here, close the window and return to Canvas for the next lesson in the series. Happy coding! 🚀
