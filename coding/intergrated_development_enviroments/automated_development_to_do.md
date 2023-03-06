# Automated Development Using Intergrated Development Enviroments

## Introduction

Integrated development environments have become very powerful in recent years. Utilising the IDE to the fullest can ensure test driven practises are stuck to as well as increasing development velocity. Don't put the emphasis on the tool rather the familiarity.

The other main to point to make about IDE's is the idea of mouse-less development. Developing code without a mouse whilst using all of the power user shortcuts ensures a slick and speedy development experience whilst minimising repetitive strain injuries.

## C# Visual Studio Code Example

This example will demonstrate the main snippets and shortcuts. Please note there are differences in shortcuts from one OS to the other. This example is using latest C# 11, XUnit and Moq as test dependencies.

### Prerequisites

- C# Development environment using this template <https://github.com/Steelstone3/C-Sharp-Project-Template>

### Steps

Creating a test class namespace

> - Create a test class in the test class project called "SpellShould.cs"
> - Type "namespace" then an auto-suggestion should appear "□ namespace". Press enter/ double tab
> - Auto completing the namespace declaration

As shown

```cs
namespace Name 
{

}
```

Changing the namespace to match the folder structure

> - To change the namespace to the actual namespace press "ctrl + ." and look for the option "change namespace to match folder structure" then press "enter"

As shown

```cs
namespace SpellGameTests.Spell
{

}
```

Creating a test class declaration

> - Type "public" then an auto-suggestion should appear "public". Press enter/ double tab
> - Type "class" then an auto-suggestion should appear "□ class". Press enter/ double tab
> - Auto completing the class declaration

As shown

```cs
namespace SpellGameTests.Spells
{
    public SpellShould 
    {
    
    }
}
```

Adding the first test

> - Type "fact" then an auto-suggestion should appear "□ Fact". Press enter/ double tab
> - Auto completing the test method declaration

As shown

```cs
namespace SpellGameTests.Spells
{
    public class SpellShould
    {
        [Fact]
        public void TestMethod()
        {
            // Given
            
            // When
            
            // Then
        }
    }
}
```

Renaming the TestMethod

NOTE: HOW TO RENAME THE TEST METHOD PRESSING F2

Initialising the unit

NOTE: PUT IN HERE ABOUT HOW TO CREATE THE CLASS YOU ARE TESTING AND ITS INTERFACE

NOTE: HOW TO CREATE A CONSTRUCTOR TO INITIALISE THE INTERFACE WITH A CLASS AND THAT THIS ALLOWS FOR THE ADDITION OF DEPENDENCIES LATER
