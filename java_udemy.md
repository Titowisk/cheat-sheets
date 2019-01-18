# Curso JAVA Udemy - Tim Buchalka

## Primitive Data Type - int, short, long, byte

Java may automatically convert types when expressions are made with different types.

Example:
```
// byte has a width of 8
byte myByteValue = -128; // smallest number
byte myByteMaxValue = 127;
byte newByte = (byte) (myByteValue/2); // cast means that I force Java to read this as a type byte
// this part "myByteValue/2" is converteded to int automatically
 ```
 
 * The propper way to declare a long type is to use "l" or "l" in the declaration:
```
 long myLongValue = 109283L;
```
 

## Primitive Data Type - Float and Double:

Java automatically convert types to double when a number have decimals.
The propper way to declare float and double is to use "F or f" and "D or d".
```
float floatValue = 5f;
double doubleValue = 5d;
```
* double is the better suggestion to use when coding (they mare more precise and are faster)

## Primitive Data Type - Char and Boolean:

Type char holds only one character or unicode caracters ('\u00A9')

## Primitive Data Type - strings:

```
String myStringValue = "bla bla bla";
```

## Operators:
https://docs.oracle.com/javase/tutorial/java/nutsandbolts/opsummary.html

Precedence order:
http://cs.bilkent.edu.tr/~guvenir/courses/CS101/op_precedence.html

Java uses The regular operators of common languages:
```
+,=, /, %, *, +=, -=, /=, *=, 
==, !=, <, >, <=, >= 
&&, || and so on
```

* It does have ternary operator too:
```
int ternary = 1 > 2 ? 5 : 10; // ternary will be 10
```
## If Else statements:

Works like any other language if(condition) {code}
```
if (condition) {
 code..
} else {
 code
}
or
if (true)
 System.out.println("Some bla bla")

```
## Methods:

*You can't put a method inside another method

- common method structure:
```
public static void calculateScore (args) {
 code...
}
```

Example:
```
public class Main {

    public static void main(String[] args) {
       	// write your code here
        saySomething("Aloha amigos");
    }

    public static void saySomething (String someText) {
        System.out.println(someText);
    }
}

```

### Method Overloading:

Using the same method name but with different args.
*This can be useful when handling different args types using the same method name

Example:
```
public static void main(String[] args) {
	// write your code here
	calculateScore("Tito", 500);
	calculateScore(1000);
}

public static int calculateScore( String playerName, int score) {
	System.out.println("Player " + playerName + " score " + score + " points");

	return  score * 1000;
}

public static int calculateScore(int score) {
	System.out.println("Unamed player score " + score + " points");

	return  score * 1000;
}
```

## Control Flow Statements:

- Switch statement:
```
Switch(option) {
	case <option1>:
		..code block..
		break;
		
	case <option2>:
		..code block..
		break;
	default: // cover all other cases
		..code block..
		break;
	...
}	
```

- For loop statement:
```
for(init; Stopcondition; increment) {
	..codeblock..
}
```

- While loop statement:

runs 0 or more times.
```
while(condition) {
	..code block..
}
```

runs 1 or more times.
```
do {
	..code block..
}while (condition);
```

*continue;
It skips to the next iteration on the loop (ignoring the rest of the code below).
```
int count = 0;
while (count < 7){

	if (count == 3){
		count += 1;
		continue;
	}
	System.out.println(count);
	count += 1;
}
Output: 0 1 2 _ 4 5 6
```

- parsing values from strings:
```
Integer.parseInt(<string>);
Double.parseDouble(<string>);
```

## Reading user input:

To read it, I must use the Scanner class (and close it after using it)

```
Scanner scanner = new Scanner(System.in);

System.out.println("Enter your year of birthday: ");
int yearOfBirth = scanner.nextInt();

scanner.close();
```

* To read user input twice, I have to add another.scannernextLine to capture the 'enter key':
```
Scanner scanner = new Scanner(System.in);

System.out.println("Enter your year of birthday: ");
int yearOfBirth = scanner.nextInt();
scanner.nextLine(); // handle next line character (enter key)

System.out.println("Enter yout name: ");
String name = scanner.nextLine();

int age = 2019 - yearOfBirth;

System.out.println( String.format("Your name is: %s and you are %d years old.", name, age) );

scanner.close();
```

## OO - parte 1:

Classes podem comunicar entre si se pertencerem a um mesmo pacote/package (pasta)
Ou se forem explicitamente importadas.

Para poderem compartilhar métodos e variáveis, é preciso gerenciar os acessos de acordo (public, private...)

```
package com.Learning;

public class Car {

    private int doors;
    private int whells;
    private String model;
    private String engine;
    private String color;

    public void setModel (String model){
        this.model = model;
    }

    public String getModel(){
        return this.model;
    }
}
```

*DICA: No intellij para gerar getters and setters é só ir em Code>Generate e escolher a opção desejada.

### Constructors:

```
public BankAccount() {
	// empty constructor
	
	// constructor with default values
	// it calls the constructor with parameters giving it the default values specified
        this("46879", 0.0, "Default", "blabla@gmail.com", "99565726"); // must be the first statement in the empty constructor
}

public BankAccount(String number, double balance, String customer, String email, String phone) {
	// constructor with parameters
	this.number = number;
	this.balance = balance;
	this.customer = customer;
	this.email = email;
	this.phone = phone;
}
```

*DICA: em constructors com parâmetros, é melhor inicializar as variáveis com o this. Se utilizar
os setters eles podem não funcionar em contexto de herança (super e sub classes).

### Method Overriding:
A sub class can overrride a method inherited from a class.

Animal class:
```
public void eat(){
        System.out.println("Animal.eat called");
}
```
    
Dog class:
```

@Override
public void eat() {
	System.out.println("Dog.eat called");
	chew();
	super.eat();
}
```

*Dica: quando usar a herança de método, é melhor chamar o método sem o ```super.```, pois caso 
a subclasse necessite sobrepor o método da super classe, o código muda automaticamente do método da super classe
para o método da subclasse.

Animal class:
```
public void move(int speed){
        System.out.println("Animal.move called. Speed = " + speed);
    }
```
Dog class:
```
public void walk(){
        System.out.println("Dog.walk() called.");
        move(5); // better then super
    }
```

### Reference x Object x Instance x Class:
Class = blueprint;
Instance = house you built using the blueprint. It is an object as well;
Object = instantiating a class means that I created an instance or object from that class;
Reference = the address of each individual house built

### super x this:
super is used to call the parent's class members (variables and methods)
this is used to call the current's class variables and methods

*they can't be used in static areas.

In the constructor the java compiler calls super() even if we don't declare it.
The super() call must be the first one inside a constructor().
The constructor can never have both super() and this() calls inside it.

*Dica: ao usar um construtor com valores default, deve-se usar o this();

- COnstructor chainning to avoid duplication of code:
```
class Rectangle {
	private int x;
	private int y;
	private int height;
	private int width;
	
	
	Rectangle (){
		this(0, 0, 0, 0); // calls 2nd constructor
		this.x = 0; // DONT
		this.y = 0: // DONT
	}
	
	Rectangle(int height, int width){
		this(0, 0, height, width); // calls 3nd constructor
	}
	
	
	Rectangle(intx, int y, int height, int width){
	// initalizes the variables
		this.x = x;
		this.y = y;
		this.height = height;
		this.width = width;
	}
}
```

### Overloading x Overriding:

Overloading = two or more methods with the same name but different paremeters
Overriding: = define a method in a child class that already exists on the parent class (same parameters)

### Static methods:
They are used to perfom actions that doesn't need any data from instances of the class.

## OO - parte 2 (composition, polymorphism and encapsulation):

- Composition:
Happens when a class has another class.
A car is a type of vehicle, I can't say vehicle has a car.
A resolution is part of the caracteristics of a monitor. A monitor HAS a resoltuion.

Example:
```
public class Monitor {
	private String model;
	private String manufacturer;
	private Resolution nativeResolution; // Monitor has a variable of the type Resolution
}

public class Resolution {
	private int width;
	private int height;
}
```

- Encapsulation:
Restrict the access (public -> private) to variables and methods to assure more control with validantions.


