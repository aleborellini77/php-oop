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
Praxis is to name the php class with each words with Capital Letter - Pascal Case way (or also example `AboutPage`).

*In object-oriented approach* to call a specific Bike with specific properties you simply instantiate in a variable an object though the generic class previously created (so the class operates as a stamp/template).
```
$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';
$bike->model = 'Gryzl';
var_dump($bike);
```
var_dump gives us the object of type Bike with the specified properties. Here lays the key concept of OOP: the idea of the possibility to call each time we want the class Bike and have different objects (bikes) instantiated.<br/>
Here we can find further difference with procedural programming: in procedural (the example done above) in an array *php* has to run through the entire array to go to the index wanted; in OOP instead, using objects, *php* has not to re-run through the entire code, but goes directly to the property/method needed. 

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
*Properties* & *Methods* are the two key concepts on which a class is based. We'll see that is possible to consider them as *variables* and *functions*.<br/>
Instead of access to properties each time using the single arrow operator we can also use/define specifical *methods* (for example if we want to combine more properties in a string to print). In procedural you had to combine access by index for each Bike (sample `$fullmodelbike = $bike['model'] . ' ' . $bike['brand'];`); instead in OOP we define in class *a specific method to return full name*.
```
class Bike {
          public $color;
          public $brand;
          public $model;

    function fullModel()
    {
        return $this->model . ' ' . $this->brand;
    }

}

$bike = new Bike;
$bike->color = 'Green';
$bike->brand = 'Canyon';

echo $bike->fullModel();
```
Two more things emerging from this last snippet: the first one that, like said above, *the single arrow operator in php OOP is used also to connect instances to related methods* (meaning you can call to an instance methods belonging to the class of that same instance); the second one is simply another note on differences between procedural and OOP, in fact this possibility to define methods inside a class to manage properties and so datas is really precious in order to have faster ways to access to datas.  

### Magic Method __construct()
When we instantiate an object for a class (for example using `$bike = new Bike`) is also possible to directly pass some parameters instantiating it.<br/>
How? Through a php *magic method* is possible to do so -> the __construct() method allows to directly pass parameters when instantiating. *This is because this magic method is automatically loaded when the class is istantiated* (it's like defining parameters to call for a mixin in SCSS/SASS).

```
function __construct($brand, $model, $color)
     {
       $this->color = $brand;
       $this->color = $model;
       $this->color = $color;
     }

$bike = new Bike('Colnago', 'G3X', 'Blue');
var_dump($bike);
```

***
> Attention: PHP lang looks at every method starting with __ (double underscore) as a **magic method**.<br/>
> Here a table with PHP main magic methods:
> | Method      | Description |
> | ----------- | ----------- |
> | __construct() | Class constructor. Called automatically when you instantiate that class. |
> | __destruct() | Class destructor. Called to destroy or to deallocate objects. |
> | __call() | Caller method to call methods that dont't exist or private ones. |
> | __callStatic() | Caller method to call static methods. |
> | __get() | Getter method to get/read inaccessible properties. |
> | __set() | Setter (🐶) method to set/write an inaccessible property. |
> | __toString() | Magic method to treat the object as a string (example in a echo) |
> | __clone() | Magic method to invoke the clone method on an object to generate a copy. |
> | others.. | Link to italian website covering the argument https://www.html.it/pag/18363/i-metodi-magici-prima-parte/ |
***

___

## 2. Visibility of properties/methods

In OOP is fundamental in order to have applications more secure and not manipulable to grant the right level of **visibility** to each property / method in a class.
The idea is that a property/method could be called/used only under the visibility rules defined in class level.
There are three levels of visibility:<br/>
- **public** --> this is the default one if nothing has been specified. The public visibility level grants that a property/method could be called outside the class (`$bike->brand = 'Canyon'`). 
- **private** --> The private visibility grants that properties/methods could be used only inside the same class.
- **protected** --> The protected level instead is a mix of the previous two: it grants the use of properties/methods inside for sure that class, but also inside other classes that comes from that same class (*inheritance* principle).

Looking at the table above covering some of the most common magic methods of php we can see that there are two methods used to get/set properties that are inaccesible (because of `private` level of visibility).<br/>
__get() and set() methods are really useful because in this way we can make accessible private properties outside the class, but, if declared in a "general way" ( __get() & __set() ), they are giving this permission to all properties and so you have to use them carefully: if you are using them, every time you add a new private property you have to add an exception (with an `if` condition to your __get() and __set() global functions). It's quite slow and verbose probably.<br/>
The best way to move here is to define a **specific getter/setter function** --> the praxis tells us to define the method using `get+NameOfPropertyInCapitalLetter` or `set+NameOfPropertyInCapitalLetter`.
```
class Bike {
    private $size;

    public getSize(): string
    {
        return $this->size;
    }

    public setSize(string $size): void
    {
      return $this->size = $size;
    }

}

$bike = new Bike;
$bike->setSize('Medium');
$bike->getSize();
var_dump($bike);
```

### Namespace

Concept introduced by php5.3.0: syntactically the namespace declaration has to be placed before class declaration; the idea is that a namespace is like a file system structure declaration used to assign each class to a specific space.<br/>
> This from php website -> "What are namespaces? In the broadest definition **namespaces are a way of encapsulating items**. In the PHP world, namespaces are designed to solve two problems that authors of libraries and applications encounter when creating re-usable code elements such as classes or functions:
> - Name collisions between code you create (internal PHP classes/functions/constants or third-party classes/functions/constants).
> - Ability to alias (or shorten) Extra_Long_Names designed to alleviate the first problem, improving readability of source code."
```
<php

namespace Mobility\MeansOfTransport\Bike;

use Mobility\MeansOfTransport;
use Mobility\MeansOfTransport\Bike;
use Mobility\MeansOfTransport\Foot as FootMobility;

class RoadBike extends Bike
{
    public function getMobilityMeansOfTransport()
    {
        return new MeansOfTransport()::getAll(); // returns an instance of Mobility\MeansOfTransport class and all means (imaging we have written a useful method to retrieve all means in that class)
    }
    public function getFootMobility()
    {
        return new FootMobility(); // returns an instance of Mobility\MeansOfTransport\Foot class (used the alias "as")
    }
    public function getCarMobility()
    {
        return new use Mobility\MeansOfTransport\Car();  // returns an instance of Mobility\MeansOfTransport\Car class (also if not used here in this class, but we have to previously had included or required this class or autoloaded them 
                                                        //  through composer autoloader)
    }
}
```

### Constants

In a class of OOP we can also (like in procedural) define a constant.
Definition of a constant differs in syntax: we define a constant in php by using `const NAMEOFCONSTANT` without any symbol like `$`(constants are case-sensitive, for praxis we name them using all capital letters or also starting/ending with __ `const __CAPITALLETTERS__`).
**To define a constant in php we use the base function `define()` and this function accepts only two params: name of constant and the value** -> `define('FAVSPORT', 'basketball')` and the values accepted are: integer, float, string, boolean or null. The idea is that defining a constant has the objective of define a fixed value that cannot change during the script or the entire application. Generally constants have global visibility.
Function to see all defined constants --> `print_r(get_defined_constants(true));`.<br/> 
**Predefined constants** are ***magic constants*** that php lang has to offer (from its core or its extensions/modules)--> for example really useful is the constant `__FILE__` that we use to get the entire path of directory to that file; or also `__DIR__` that prints only the directory path (without that file).

From php5 it is possible to define a constant also in a class. The **big difference with properties and methods of a class** is that **a constant of a class doesn't belong to the instance of that class** (such as props and methods); instead **the constant of a class belongs only to the class so it is callable only inside classes** (for this reason we cannot use $this to refer to constants or use the -> operator to refer to them from outside).
```
class Bike {
    public $countryOfStore;
    const BIKESHOP = 'Padova Canyon Bikestore';

    public function getBikeShop()
    {
       return self::BIKESHOP;
    }

    public function getBikeShopComplete()
    {
       return $this->countryOfStore . ', ' . Bike::BIKESHOP;
    }

}
$bike = new Bike;
$bike->countryOfStore = 'Italy';
$bike->getBikeShopComplete();
echo $bike;
```
As seen above we can access to the constant inside the class in two ways: by using `self` or `the name of the class` followed by `::` the **scope operator**.
> From **php8.3** we can define the type of a constant in its definition -> `const string BASKETBALLTEAM = 'Dallas Mavericks'`. This is useful from the point of view of security (language more typified) and it gives us the possibility to redefine the same constant in an extended class (only if it is of the same type, example a string).
> ```
> class One {
>    const string NAME = "Simone Fontecchio";
>  }
> class AnotherOne {
>    const NAME = "Gigi Datome";
>  }
> ```   

___

## 3. Inheritance
Inheritance concept is at the basis of OOP in php: **a class can inherit properties and methods by a parent class (and so being child class of that one)**. The child class can implement new specific properties and methods, but also can *override* properties/methods of parent class (through *overriding technique*). 
Important note: **in php a class can extend another one, but just one** (not two or more). This explains *interfaces/traits* existence (as we'll see, interfaces/traits can be implemented more than one at a time, allowing a sort of *multiple inheritance*).   
`extends` is the keyword to use for inheritance.

```
	class Bike {
			public $color; // public visibility
			protected $brand; // visible in parent class and child ones
			private $id_frame; // private, so visible only on this class
			// constructor
			public function __construct()
			{
				echo "Calling parent class constructor"."<br>";
				// init of $color property
				$this->color = "Red";
			}	
			// methods
			public function getColor() {
				return $this->color;
			}				
			public function setIdFrame($id_frame) {
				// set id_frame
				 $this->id_frame = $id_frame;
			}
	}

	// child class definition
	class RoadBike extends Bike {
		public $model;
		public function __construct($model, $id_frame) // child class constructor
		{
			$this->setIdFrame($id_frame);
			$this->model = $model; // init of new property of child class
		}	
		function setBrand(string $brand) {
			$this->brand = $brand;
		}
	}

	// instance of new object from Bike class
	$bike = new Bike();
	echo "Bike: ".$bike->getName()."<br />";
	$roadBike = new RoadBike("AERoad","943852861950001324");
	$roadBike->color = "Yellow";
	$roadBike->setBrand('Canyon');
	// print associative array of the object
	print_r(get_object_vars($bike));
	print_r(get_object_vars($roadBike));

```

In the example above we can see some of the main features that *inheritance* brings to us: RoadBike class is an extension of Bike class (child class & parent class); we can see that properties (called also attributes) and methods from parent class has been inherited by child class (public and protected). Instead, the private property declared in parent class Bike has been used in a public method defined inside the same class for a reason: this allowed to get this private attribute through the use of the public method of parent class ($id_frame, setIdFrame()).

**Overriding technique**<br/>
It is based on this syntax:
```
<?php
...
parent::methodToOverride();
...
?>
```
So we can call parent class through the keyword `parent` + the scope operator `::` + the method to override. This is when we call a method but not in traditional way, using instead the scope operator and the parent class.<br/>
In general we use the *override technique* to simply recall a method or to override it (for example adding stuff to it).
```

	class Bike {
			public $color;
			protected $brand; 
			private $id_frame; 
			
			public function getColor() {
				return $this->color;
			}				
			public function setIdFrame($id_frame) {
				// set id_frame
				 $this->id_frame = $id_frame;
			}
	}

	class RoadBike extends Bike {
		public $model;
			
		function getColor() {
                     parent::getColor();
		     echo $this->model . '' . parent::setIdFrame($id_frame); 		
		}
	}
```

> Constructor & destructor magic methods of php are inherited by child classes by default (but you can also override them if you need it! -> example: if you want to add a parameter to pass to the constructor method for the subclass/child class).

`final` keyword -> is used to prevent the inheritance mechanism: in fact when you prepend to method or also class declaration the *final* keyword you are blocking the inheritance mechanism (if we try to extend a final class, we get a php error telling us that is prohibited  to extend a *final class*). 

___

## 4. Multiple Inheritance



