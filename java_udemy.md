# Curso JAVA Udemy - Tim Buchalka

## Primitive Data Type - int, short, long, byte

Java may automatically convert types when expressions are made with different types.

Example:
```
// byte has a width of 8
byte myByteValue = -128; // smallest number
byte myByteMaxValue = 127;
byte newByte = (byte) (myByteValue/2); // cast means that I force Java to read this as a type byte
// this part myByteValue/2 is converteded to int automatically
 ```
