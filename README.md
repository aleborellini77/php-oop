# PHP - Object Oriented Programming (OOP)
___
 
Notes and code snippets just to get my thoughts in order. Take them if you need it ⛽<br/>
(Sorry for Eng possible mistakes 🔠) 

___

### Short introduction

> Why not procedural programming ?

The idea behind the Object Oriented approach is to allow to create a development environment where you can have more complexity & scalability at same time.<br/>
*Procedural programming* executes commands in a linear order, based on the order you have written your code; instead *OOP* is based on the concept of *Classes* and code is not executed linearly (thanks to concepts like *inheritance* and *polymorphism*).<br/>
For sure procedural approach is faster and simpler (and also still the right choice when you have to face simple programming), but when you have to face more complex applications the better road to follow is the OOP one. Through OOP you can organize the work in a team assigning one of the different fields of the application through *classes*, achieving a code more maintainable.

___

### 1. Class concept

> Short Definition: 
> A *class* is a stamp (or a template) that identify an instantiated object that we want to link to properties and specifical functions to manipulate its datas or other infos. So the class is the stamp/template of what (through the OOP approach) we want to represent in code as an object.<br/>

It's really claryfing to me this idea: example, we are speaking about Bikes, *in a procedural approach* to call a specific Bike with its properties you have to create a variable `$bike` containing an associative array, instead OOP allows you to use the generic class created to instantiate that $bike.

```
class Bike {
          public $color;
          public $brand;
          public $model;
}
```
Praxis is to name the class with first Capital letter (or also example `AboutPage`).

*In object-oriented approach* to call a specific Bike with specific properties you simply instantiate an object though the generic class created (so the class operates as a stamp/template).
```
$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';
$bike->model = 'Gryzl';
var_dump($bike);
```
Note: we have used a **special arrow operator (->)** to call properties to the object; this is possible because of the `public` declaration of the property in this class.

#### Main features of a class
*Properties* & *Methods* are the two key concepts on which a class is based.


