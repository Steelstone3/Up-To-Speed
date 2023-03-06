# Clean Code

Clean code is a set of principles and practices that aim to improve the readability, maintainability, and overall quality of software code. The concept of clean code emphasizes the importance of writing code that is easy to understand, modify, and extend, while minimizing complexity, redundancy, and technical debt.

Some key principles of clean code include using meaningful names for variables, functions, and classes, keeping functions and classes small and focused on a single responsibility, avoiding global state and side effects, reducing duplication and unnecessary complexity, and writing code that is well-organized, well-structured, and easy to follow.

Clean code practices also include the use of appropriate formatting, commenting, and documentation, as well as the adoption of code reviews, testing, and refactoring to continuously improve the codebase.

## Benefits

The benefits of clean code include increased productivity, reduced development time, improved collaboration and code reuse, better error handling and debugging, and increased user satisfaction with the software product.

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

There is plent of dirty code within the first implementation. Clean code aims to get the minimum viable implementation to meet the functional and non-functional requirements.

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

## Summary

Overall, clean code is an essential aspect of software development, as it helps to ensure that the codebase is maintainable, scalable, and adaptable to changing requirements over time.
