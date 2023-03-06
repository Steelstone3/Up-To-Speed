# YAGNI

## Introduction

(YAGNI) You Ain't Gonna Need It is a principle in software development that suggests that developers should not add functionality to their code until it is necessary. The idea behind YAGNI is that it is often difficult to predict what features will be needed in the future, and attempting to add them prematurely can lead to wasted time and effort.

YAGNI can also be used as the underlying concept for [clean code](./clean_code.md) in the removal of waste and un-needed code.

the YAGNI principle encourages developers to be pragmatic and avoid wasting time on unnecessary features or functionality. By focusing on delivering working code that meets the current requirements to the precise acceptance critria laid out.

## Example

Lets take the classic example of calculating areas of different shapes in OOP.

### Acceptance Criteria

> Provide a triangle and square with a public function to return the area as an integer.

### Implementation (Dirty)

```C#
interface IShape 
{
    int Height { get; }
    int Width { get; }
    int Area { get; }
    int CalculateArea();
}

class Square : IShape() 
{
    public Square(int height, int width)
    {
        Height = height;
        Width = width;
        // Pointless assignment
        Area = 0;
    }

    // 0 External references
    public int Height { get; }
    public int Width { get; }
    public int Area { get; }

    public int CalculateArea()
    {
        Area = Height * Width;
        return Area;
    }
}

// Pointless class (not in functional requirements)
class Rectangle : IShape() 
{
    public Rectangle(int height, int width)
    {
        Height = height;
        Width = width;
        // Pointless assignment
        Area = 0;
    }

    // 0 External references
    public int Height { get; }
    public int Width { get; }
    public int Area { get; }

    public int CalculateArea()
    {
        Area = Height * Width;
        return Area;
    }
}

class Triangle : IShape() 
{
    public Triangle(int height, int baseOfTriangle)
    {
        Height = height;
        Width = baseOfTriangle;
        // Pointless assignment
        Area = 0;
    }

    // 0 External references
    public int Height { get; }
    public int Width { get; }
    public int Area { get; }

    public int CalculateArea()
    {
        Area = Height * (Width/2);
        return Area;
    }
}
```

### Implementation (Clean)

There is plent of YAGNI in these classes. Lets look at what this could look like once YAGNI has been applied retroactively.

```C#
// The interface has been taken to its minimal implementation 
interface IShape 
{
    int CalculateArea();
}

class Square : IShape
{
    // Removal of additional parameter square doesn't need
    // Encapuslation of sideLength
    private readonly int sideLength;

    public Square(int sideLength)
    {
        this.sideLength = sideLength;
    }

    // Removed unused properties

    // Refactored calculation
    // Expression body
    public int CalculateArea() => Math.Pow(sideLength, 2);
}

// Rectange is gone because it wasn't part of the functional requirements

class Triangle : IShape() 
{
    // Encapuslation of height and baseOfTriangle
    private readonly int height;
    private readonly int baseOfTriangle;

    public Triangle(int height, int baseOfTriangle)
    {
        this.height = height;
        this.baseOfTriangle = baseOfTriangle;
    }

    // Removed unused properties

    // Expression body
    public int CalculateArea() => height * (baseOfTriangle/2);
}
```

It is important to keep YAGNI in mind whilst programming. However it can be hard to keep this in active memory so a focused effort of refactoring will ensure the code fits this principle.
