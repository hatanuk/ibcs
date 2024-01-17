
## Encapsulation
Encapsulation is a method for introducing **modularity** into your code; ie. it serves the purpose of keeping sections of the code (in this case, classes) self-contained and the inner workings abstracted away. 
Encapsulation can be achieved through the use of the **private** *access modifier*, which prevents the variable or method from being accessed externally.

*(**external** code refers to code outside of a specific class (such as in the main() method) and **internal** refers to the code found inside of the class)*

For example,
```java

private int length = 5;
```


An *access modifier* is the first keyword you type whenever defining a variable or method. The two access modifiers we have learned so far are **private** and **public**.
So, what is the difference?
Let's say we define a class called *Circle* with two double variables, *radius* and *PI*. In the constructor, we accept a parameter to set *radius* when creating an instance. 
```java
class Circle {

    public double radius;
    private double PI = 3.14159;
	
    public Circle(double radius) {
        this.radius = radius;
    }
}
```
The difference between the two variables *radius* and *PI* is the access modifier, **public** and **private**. Let's try to create an instance of this class and access the two variables.
```java
Circle myCircle = new Circle(5);

System.out.println(myCircle.radius); // This works: output is 5.0
	
System.out.println(myCircle.PI); // Error while compiling, the private variable "is not visible".
```

As you can see, you cannot access, or "see",  the **private** variable *PI*. However, you would still be able to access the variable internally.
```java
class Circle {
    // Rest of the code...
	    
    public double getArea() {
        return 2 * PI * radius;
    }
}
```
Since the method *getArea()* is located inside of the class, the private variable *PI* is able to be accessed and even changed. 

## Getters and Setters
There exists an alternative method to access and change **private** variables outside of their class. These methods, called Getters (for *returning* a **private** variable) and Setters (for *changing* a **private** variable), are defined within the class itself.

You might wonder, why is it necessary to have a method to set & get **private** variables, when you could just make them **public** and alter them manually? The reason is that Getters & Setters can include additional procedures that are executed whenever a variable is changed or returned. 

For example, let's say we have a class Square with two variables, *length* and *area*. In the constructer, a parameter is accepted for *length*, and *area* is calculated using the same parameter.
```java
class Square() {

    public double length;
    public double area;

    public Square(double length) {
        this.length = length;
        area = length * length;
    }
}

```
If some other part of the code would like to change the variable *length* after the object has been instantiated, without Getters and Setters, there could be some issues. 

```java

Square mySquare = new mySquare(2);
mySquare.length = 5;
	
System.out.println(mySquare.length); // outputs 5.0
System.out.println(mySquare.area); // outputs 4.0
```

Something doesn't seem right. Although *length* was updated, the *area* remains unchanged. If you didn't know how *Square* was implemented, or simply forgot to change the area as well, this could easily lead to errors. This type of code is **not modular**, as the implementation of *Square* is not well abstracted. 

The issue could be avoided by making the two variables **private**, and adding some extra behaviour to the Setter method. We need to make some Getter methods too, in order to be able to access the variables.

 ```java	
// Setters
 public void setLength(double length) {
	// Change the length variable
	this.length = length;
	// But ALSO change the area variable
	area = length * length;
}
	
// Getters
public double getLength() {
	return length;
}
public double getArea() {
	return area;
}

```

Now, the *area* variable changes correspondingly!
```java   
Square mySquare = new mySquare(2);
mySquare.setLength(5);
    
System.out.println(mySquare.getLength()); // outputs 5.0
System.out.println(mySquare.getArea()); // outputs 25.0
```
Hopefully you are able to see the advantages of using the **private** modifier, Setters, and Getters in building **modular** code.

## Uses of Encapsulation
To recap, here are the ways to implement encapsulation in your code, and the benefits of doing so:

**1) Data Hiding**\
By using the **private** modifier on variables, in combination with Getters and Setters, we are able to control them to be:
- Read-only (Getters)
- Write-only (Setters)
- Read and write (Getters and Setters)
- Neither, for use only inside the class (None)

Similarly, we can apply the **private** modifier to methods, which prevents unintended usage of them outside of the class.
Data hiding provides many advantages, such as:
- Improving runtime **security** by preventing external access to certain methods/variables
- Communicating the proper usage of a class, increasing **collaboration** and **readability**
- Preventing unintended external usage that may lead to errors (a form of **validation**, improving **robustness**)
- Allowing for code **reusability** using methods inside the class that shouldn't otherwise be accessed externally

**2) Abstraction**\
Additionally, by using **private** modifier on variables or methods, we are able to build our code in a way that hides implementation details (such as by adding extra behaviour to your Getters/Setters), which leads to abstraction.
Abstraction is useful because it allows us to focus on the bigger picture; we can quickly reuse code without having to worry about the small details.\
Some advantages of abstraction are:


- Increases the **reusability** of the code; abstracted code fits more use cases
- Detail is reduced, increasing **readability**
-  Allows for multiple programmers to use each other's code without knowing the implementation (**collaboration**)
- Encourages **modular** code

**3) Modularity**\
Structuring your code in an encapsulated way is a good way to increase the modularity of your code. This is because encapsulated code (such as that contained in classes) can be considered as being sorted into "modules", as the code inside the class is seperate from the code outside.
Modularity is probably one of the most important aspects of writing good code!\
Here are some benefits:
- Allows multiple programmers to work on separate snippets of code *at the same time*, improving **collaboration**
- Organization is improved, meaning higher **readability**
- Reduces the need to change external code when changing internal functionality (easier **maintenance**)
- Easier **debugging**, as errors can be traced back to a specific module
- Improved **testability**, as modules can be tested to work separately from external code.
- **Decomposition**. Breaking your code into many smaller modules helps solve larger problems
