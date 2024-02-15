# PHP - Object Oriented Programming (OOP)
___
 
Notes and code snippets just to get my thoughts in order. Take them if you need it ⛽<br/>
(Sorry for Eng possible mistakes 🔠) 

___

## Short introduction

> Why not procedural programming ?

The idea behind the Object Oriented approach is to allow to create a development environment where you can have more complexity & scalability at same time.<br/>
*Procedural programming* executes commands in a linear order, based on the order you have written your code; instead *Object-Oriented Programming* is based on the concept of *Classes* and code is not executed linearly (thanks to concepts like *inheritance* and *polymorphism*).<br/>
For sure procedural approach is faster and simpler (and also still the right choice when you have to face simple programming), but when you have to face more complex applications the better road to follow is the OOP one. Through OOP you can organize the work in a team assigning one of the different fields of the application through *classes*, achieving a code more maintainable.

___

## 1. Class concept

> Short Definition: 
> A *class* is a stamp (or a template) that identify an instantiated object that we want to link to properties and specifical functions to manipulate its datas or other infos. So the class is the stamp/template of what (through the OOP approach) we want to represent in code as an object.<br/>

It's really claryfing to me this idea: example, we are speaking about Bikes, *in a procedural approach* to call a specific Bike with its properties you have to create a variable `$bike` containing an associative array, instead OOP allows you to use the generic class created to instantiate that $bike.

How to declare a class -> class NameOfClass {properties & methods}
```
class Bike {
          public $color;
          public $brand;
          public $model;
}
```
Praxis is to name the class with first Capital letter (or also example `AboutPage`).

*In object-oriented approach* to call a specific Bike with specific properties you simply instantiate in a variable an object though the generic class previously created (so the class operates as a stamp/template).
```
$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';
$bike->model = 'Gryzl';
var_dump($bike);
```
var_dump gives us the object of type Bike with the specified properties. Here lays the key concept of OOP: the idea of the possibility to call each time we want the class Bike and have different objects (bikes) instantiated.<br/>
Here we can find further difference with procedural programming: in procedural (the sample done above) in an array *php* has to run through the entire array to go to the index wanted; in OOP instead, using objects, *php* has not to re-run through the entire code, but goes directly to the property/method needed. 

Note: we have used the **single arrow operator (`->`,  operator for assignment of a value to a variable or a constant != from `=>`, that is the operator for key/value assignment)** to call properties to the object and assign a value to them; this is possible because of the `public` declaration of the property in this class.<br/>
ed. `->` This is also referred to as the **object operator**, or sometimes the single arrow operator.
It is an access operator used **for access/call methods and properties in a PHP object** in Object-Oriented Programming (OOP).


### Cloning
Attention to the idea of `instance` -> *the object is the instance of a class ok, but we have go deeper and say that precisely **the instance is only a pointer to that class** and not the class itself*. This means that we cannot clone an instance of a class ( sample doing `$bike2 = $bike` and pretend to assign through object operator values to the class properties and have different results/values). In fact to clone correctly an instance/object you have to use the php command `clone`.
```
class Bike {
          public $color;
          public $brand;
          public $model;
}

$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';
$bike->model = 'Gryzl';

$bike2 = clone $bike;
$bike2->color = 'yellow';
$bike2->brand = 'Specialized';
$bike2->model = 'S-Gravel';

var_dump($bike);
var_dump($bike2);
```
 

### Main features of a class
*Properties* & *Methods* are the two key concepts on which a class is based.<br/>
Instead of access to properties each time using the single arrow operator we can also use/define specifical *methods* (for example if we want to combine more properties in a string to print). In procedural you had to combine access by index for each Bike (sample `$fullmodelbike = $bike['model'] . ' ' . $bike['brand'];`); instead in OOP we define in class a specific method to return full name.
```
class Bike {
          public $color;
          public $brand;
          public $model;

    function fullModel() {
        return $this->model . ' ' . $this->brand;
    }

}

$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';

echo $bike->fullModel();
```
Two more things emerging from this last snippet: the first one that, like said above, the single arrow operator in php OOP is used also to connect instances to related methods (meaning you can call to an instance methods belonging to the class of that same instance); the second one is simply another note on differences between procedural and OOP, in fact this possibility to define methods inside a class to manage properties and so datas is really precious in order to have faster ways to access to datas.  

