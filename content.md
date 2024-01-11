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

There are times when it makes sense to auto-create just a setter OR just a getter for an attribute (not both). Ruby also has `attr_reader` for creating getter methods and `attr_writer` for creating setter methods.

### Custom Setters and Getters
Sometimes, you need more control over how attributes are set or retrieved. In these cases, you can define custom setter and getter methods.

For instance, you might want to ensure that a person's name is always stored in title case:

```ruby
class Person
  attr_reader :first_name, :last_name, :role

  def initialize(first_name, last_name, role)
    # we use 'self' here (instead of @) to refer to our custom setter method for first_name
    # this way it will be capitalized during initialization
    self.first_name = first_name
    @last_name = last_name
    @role = role
  end

  def first_name=(value)
    # to be prevent errors, we only allow first_name to be a String
    unless value.is_a?(String)
      raise TypeError, 'First name must be a string'
    end

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

# Change and then print the make
car.make = "ford"
pp car.make

# Change and then print the model
car.model = "explorer"
pp car.model

# Change and then print the year
car.year = 2022
pp car.year

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
end
```
{: .repl-test #car_class_test_1 for="car_class" title="Car Class initializes with make, model, and year" points="1"}

```ruby
describe "Car class" do
  it "allows changing the make and stores it in uppercase" do
    car = Car.new("Toyota", "Camry", 2021)
    car.make = "toyota"
    expect(car.make).to eq("Toyota")
  end
end
```
{: .repl-test #car_class_test_2 for="car_class" title="Car Class allows changing the make and stores it in uppercase" points="1"}

```ruby
describe "Car class" do
  it "allows changing the model and stores it in uppercase" do
    car = Car.new("Toyota", "Camry", 2021)
    car.model = "corolla"
    expect(car.model).to eq("Corolla")
  end
end
```
{: .repl-test #car_class_test_3 for="car_class" title="Car Class allows changing the model and stores it in uppercase" points="1"}

```ruby
describe "Car class" do
  it "allows changing the year" do
    car = Car.new("Toyota", "Camry", 2021)
    car.year = 2022
    expect(car.year).to eq(2022)
  end
end
```
{: .repl-test #car_class_test_4 for="car_class" title="Car Class allows changing the year" points="1"}

```ruby
describe "Car class" do
  it "only allows the year to be an integer" do
    car = Car.new("Toyota", "Camry", 2021)
    expect { car.year = "corolla" }.to raise_error(TypeError)
  end
end
```
{: .repl-test #car_class_test_5 for="car_class" title="Car Class only allows the year to be an integer" points="1"}

## Summary
Understanding initializers and how to customize setters/getters in Ruby is essential for creating flexible and robust object-oriented applications. These concepts allow for more control over how data is handled within your objects, leading to cleaner and more maintainable code.

Happy coding, and see you in the next lesson! 🚀
