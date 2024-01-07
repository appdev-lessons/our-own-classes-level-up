# Our own classes: level up

## Initializers

Initializing an object with data is a common practice in object-oriented programming. Ruby's initialize method is called automatically when a new object is created, allowing us to set initial values for the object's attributes.

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

## Setters and Getters: Auto-creation and Customization
Ruby provides `attr_accessor` for automatically creating basic setters and getters. However, there are scenarios where you might want to customize these methods.

### Auto-Creation with attr_accessor
`attr_accessor` is a Ruby method that creates both setter and getter methods for the specified attributes. It's a convenient shorthand for defining these methods manually.

For example:

```ruby
class Person
  attr_accessor :first_name, :last_name
end

person = Person.new
person.first_name = "Ian"
pp person.first_name
```
{: .repl #person_attr_accessor title="Person attr_accessor" points="1"}

### Custom Setters and Getters
Sometimes, you need more control over how attributes are set or retrieved. In these cases, you can define custom setter and getter methods.

For instance, you might want to ensure that a person's name is always stored in title case:

```ruby
class Person
  attr_reader :first_name, :last_name, :role

  def initialize(first_name, last_name, role)
    self.first_name = first_name
    @last_name = last_name
    @role = role
  end

  def first_name=(value)
    raise TypeError, 'First name must be a string' unless value.is_a?(String)

    @first_name = value.capitalize
  end

  # TODO: do the same for :last_name
end

person = Person.new("ian", "Heraty", "Instructor")
pp person.first_name # "Ian"
person.first_name = "ian"
pp person.first_name # "Ian"
```
{: .repl #person_custom_setter_getter title="Person Custom Setters and Getters" points="1"}

## Practice with Initializers and Setters/Getters
Let's put these concepts into practice. Define a Car class with the following requirements:

It should have make, model, and year attributes.
Use an initializer to set these attributes when a new Car object is created.
Also, create explicit setter and getter methods for these attributes.
Here's a skeleton to help you start:

```ruby
class Car
  attr_reader :make, :model, :year

  def initialize(make, model, year)
    # TODO: initialize attributes
  end

  # TODO: Custom setters for make, model, and year
end

# Test your Car class
car = Car.new("toyota", "camry", 2021)
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
    car = Car.new("toyota", "camry", 2021)
    expect(car.make).to eq("Toyota")
    expect(car.model).to eq("Camry")
    expect(car.year).to eq(2021)
  end

  it "allows changing the model and stores it in uppercase" do
    car = Car.new("Toyota", "Camry", 2021)
    car.model = "corolla"
    expect(car.model).to eq("Corolla")
  end

  it "only allows the year to be an integer" do
    car = Car.new("Toyota", "Camry", 2021)
    expect { car.year = "corolla" }.to raise_error(TypeError)
  end
end
```
{: .repl-test #car_class_test for="car_class" title="Car Class Tests" points="1"}

## Summary
Understanding initializers and how to customize setters/getters in Ruby is essential for creating flexible and robust object-oriented applications. These concepts allow for more control over how data is handled within your objects, leading to cleaner and more maintainable code.

Happy coding, and see you in the next lesson! 🚀
