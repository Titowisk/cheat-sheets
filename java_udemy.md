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

* You can't put a method inside another method

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
