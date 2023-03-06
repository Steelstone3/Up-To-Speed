# Datatypes & Defaults

## Introduction

C# is a strongly typed language, which means that all variables must have a specific type assigned to them. C# provides a range of built-in data types that developers can use to declare and manipulate variables.

## Primative Types

Type | Represents | Range | Default Value
:-- | :--: | :--: | :--:
bool | Boolean value | True or False | False
byte | 8-bit unsigned integer | 0 to 255 | 0
char | 16-bit Unicode character | U +0000 to U +ffff | '\0'
decimal | 128-bit precise decimal values with 28-29 significant digits | (-7.9 x 1028 to 7.9 x 1028) / 100 to 28 | 0.0M
double | 64-bit double-precision floating point type | (+/-)5.0 x 10-324 to (+/-)1.7 x 10308 | 0.0D
float | 32-bit single-precision floating point type | -3.4 x 1038 to + 3.4 x 1038 | 0.0F
int | 32-bit signed integer type | -2,147,483,648 to 2,147,483,647 | 0
long | 64-bit signed integer type | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0L
sbyte | 8-bit signed integer type | -128 to 127 | 0
short | 16-bit signed integer type | -32,768 to 32,767 | 0
uint | 32-bit unsigned integer type | 0 to 4,294,967,295 | 0
ulong | 64-bit unsigned integer type | 0 to 18,446,744,073,709,551,615 | 0
ushort | 16-bit unsigned integer type | 0 to 65,535 | 0

## Object Types

Type | Represents | Default Value
:-- | :--: | :--:
Class | a template to create objects | null
String | an array of char to represent text | null
