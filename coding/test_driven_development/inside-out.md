# Inside-Out

## Introduction

Inside-out test driven development is the process of developing software from the detail to the overarching design architecture.

By focusing on units of code the risks for bugs within each tested unit are reduced. In addition the code quality can be easily improved as any implementation that doesn't break the tests is valid allowing for a concept known as "clean code".

## Best Practise

* Focus on covering the public interface of each class (public methods)
* Ensure edge case behaviours are covered in the tests by thinking about the ways in which the method can be used and abused
* When driving an algorithm consider using a "theory" type of test. This is a test that takes parameters for testing variations.

## Example

Inside-out test driven development is best placed when working through the behaviours of a unit. This can be demonstrated with the Roman Numeral Kata. Follow along with the steps in the example following the red, green, refactor, repeat process.

### Kata

Roman Numeral kata. Create a solution that converts decimal to roman numeral from 1 - 3999. The public interface of the method should return a string and take a integer to convert.

Git clone this template <https://github.com/Steelstone3/C-Sharp-Project-Template>

Create a file called RomanNumeralConverterShould.cs in the test project and a file called RomanNumeralConverter in the application project. Remove all other files besides program.cs.

### Steps

Write a test that checks for edge cases. In this case support for convertion will be in the ranges of 1-3999.

This first test checks one of these cases.

```cs
{
    {
        [Fact]
        public void ConvertToRomanNumeralThrowsAnException()
        {
            // Given
            IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

            // Then
            Assert.Throws<ArgumentOutOfRangeException>(() => romanNumeralConverter.ConvertToRomanNumeral(0));
        }
    }
}
```

The simplest implementation for making this test pass is the following.

```cs
{
    {
        public void ConvertToRomanNumeral(int convertedNumber) => throw new ArgumentOutOfRangeException();
    }
}
```

In this instance there is nothing to refactor. Commit this as the first step towards a solution. This will allow for "returning to green".

Lets expand the test to cover the other exception cases. For this a theory type test can be used.

```cs
{
    {
        [Theory]
        [InlineData(0)]
        [InlineData(-1)]
        [InlineData(4000)]
        public void ConvertToRomanNumeralThrowsAnException(int convertionNumber)
        {
            // Given
            IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

            // Then
             Assert.Throws<ArgumentOutOfRangeException>(() => romanNumeralConverter.ConvertToRomanNumeral(convertionNumber));
        }
    }
}
```

None of the additional test break the current implementation but cover the remaining edge cases.

Now lets write a new failing test.

```cs
{
    {
        [Fact]
        public void ConvertToRomanNumeralReturnsIWhenInputIs1()
        {
            // Given
            IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

            // When
            string result = romanNumeralConverter.ConvertToRomanNumeral(1);

            // Then
            Assert.Equal("I", result);
        }
    }
}
```

and the minimum implementation to make the test pass.

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            if (decimalNumber < 1 || decimalNumber > 3999)
            {
                throw new ArgumentOutOfRangeException();
            }

            return "I";
        }
    }
}
```

Now for the refactoring step what can be done here?

For the tests both tests share the roman numeral converter. This can be made into a private variable as for each test ran in xunit a new instance is created.

```cs
{
    {
        private readonly IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

        [Theory]
        [InlineData(0)]
        [InlineData(-1)]
        [InlineData(4000)]
        public void ConvertToRomanNumeralThrowsAnException(int convertionNumber)
        { ... }

        [Fact]
        public void ConvertToRomanNumeralReturnsIWhenInputIs1()
        { ... }
    }
}
```

For the implementation the clarity of the arguement out of range exception if statement could be made clearer.

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            bool isLessThanMinimumRange = decimalNumber < 1;
            bool isGreaterThanMaximumRange = decimalNumber > 3999;

            if (isLessThanMinimumRange || isGreaterThanMaximumRange)
            {
                throw new ArgumentOutOfRangeException();
            }

            return "I";
        }
    }
}
```

This makes the code more readable and reduces the need for comments.

Moving on... add the next most obvious test

```cs
{
    {
        private readonly IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

        [Fact]
        public void ConvertToRomanNumeralReturnsIIWhenInputIs2()
        {
            // When
            string result = romanNumeralConverter.ConvertToRomanNumeral(2);

            // Then
            Assert.Equal("II", result);
        }
    }
}
```

Now make the implementation pass

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            bool isLessThanMinimumRange = decimalNumber < 1;
            bool isGreaterThanMaximumRange = decimalNumber > 3999;

            if (isLessThanMinimumRange || isGreaterThanMaximumRange)
            {
                throw new ArgumentOutOfRangeException();
            }

            switch (decimalNumber)
            {
                case 2:
                    return "II";
                default:
                    return "I";
            }
        }
    }
}
```

Now consider what refactoring can be done

Firstly for the tests another theory can be created "I" and "II" cases as well as any future additional case for coverting numerals to roman numerals. Note that as the solution gets more specific the tests become more generic.

```cs
{
    {
        private readonly IRomanNumeralConverter romanNumeralConverter = new RomanNumeralConverter();

        [Theory]
        [InlineData(1, "I")]
        [InlineData(2, "II")]
        public void ConvertToRomanNumeralReturnsRomanNumeralWhenInputIsDecimal(int numeral, string expectedRomanNumeral)
        {
            // When
            string romanNumeral = romanNumeralConverter.ConvertToRomanNumeral(numeral);

            // Then
            Assert.Equal(expectedRomanNumeral, romanNumeral);
        }
    }
}
```

For the implementation when there is an obvious pattern refator towards that design. Otherwise write another test to triangulate the implementation. In this example it is clear that if "III" was added to the theory test then another case in the switch statement would need to be added. This means that our program is static and in general the ideal solution would use an algorithm to perform the conversion.

The refactor for this step is as follows... Firstly convert to roman numeral as a method was becoming large so a method to do one thing has been extracted to check the range is valid. Secondly the pattern emerging was incrementing the number of "I" based on the decimal... hence a for loop

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            CheckValidRange(decimalNumber);

            string romanNumeral = string.Empty;

            for (int i = 0; i < decimalNumber; i++)
            {
                romanNumeral += "I";
            }

            return romanNumeral;
        }

        private static void CheckValidRange(int decimalNumber)
        {
            bool isLessThanMinimumRange = decimalNumber < 1;
            bool isGreaterThanMaximumRange = decimalNumber > 3999;

            if (isLessThanMinimumRange || isGreaterThanMaximumRange)
            {
                const string OUT_OF_RANGE_EXCEPTION_MESSAGE = "Decimal number must be between 1 and 3999.";
                throw new ArgumentOutOfRangeException(nameof(decimalNumber), OUT_OF_RANGE_EXCEPTION_MESSAGE);
            }
        }
    }
}
```

Our solution at the moment will output "IIII" for 4 and "IIIII" for 5. In roman numerals this isn't correct so a new test is needed to expose this. Lets add another test to the theory remembering to keep to 1 failing test at a time.

```cs
{
    {
        [Theory]
        [InlineData(1, "I")]
        [InlineData(2, "II")]
        [InlineData(3, "III")]
        [InlineData(5, "V")]
        public void ConvertToRomanNumeralReturnsRomanNumeralWhenInputIsDecimal(int numeral, string expectedRomanNumeral)
        {
            // When
            string romanNumeral = romanNumeralConverter.ConvertToRomanNumeral(numeral);

            // Then
            Assert.Equal(expectedRomanNumeral, romanNumeral);
        }
    }
}
```

and the implementation

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            CheckValidRange(decimalNumber);

            string romanNumeral = string.Empty;

            for (int i = 0; i < decimalNumber; i++)
            {
                romanNumeral += "I";

                if (romanNumeral.Contains("IIIII"))
                {
                    romanNumeral = "V";
                }
            }

            return romanNumeral;
        }
    }
}
```

Add another failing test

```cs
{
    {
        [Theory]
        [InlineData(1, "I")]
        [InlineData(2, "II")]
        [InlineData(3, "III")]
        [InlineData(5, "V")]
        [InlineData(4, "IV")]
        public void ConvertToRomanNumeralReturnsRomanNumeralWhenInputIsDecimal(int numeral, string expectedRomanNumeral)
        {
            // When
            string romanNumeral = romanNumeralConverter.ConvertToRomanNumeral(numeral);

            // Then
            Assert.Equal(expectedRomanNumeral, romanNumeral);
        }
    }
}
```

and the simplest implementation

```cs
{
    {
        public string ConvertToRomanNumeral(int decimalNumber)
        {
            CheckValidRange(decimalNumber);

            string romanNumeral = string.Empty;

            for (int i = 0; i < decimalNumber; i++)
            {
                romanNumeral += "I";

                if (romanNumeral.Contains("IIII"))
                {
                    romanNumeral = "IV";
                }
                else if (romanNumeral.Contains("IVI"))
                {
                    romanNumeral = "V";
                }
            }

            return romanNumeral;
        }
    }
}
```

A pattern is starting to emerge again so lets refactor into a new more generic solution

```cs
{
    {
        private readonly Dictionary<int, string> DecimalToRoman = new()
        {
            { 5, "V" },
            { 4, "IV" },
            { 1, "I" },
        };

        public string ConvertToRomanNumeral(int decimalNumber)
        {
            CheckValidRange(decimalNumber);

            string romanNumeral = string.Empty;

            foreach (var item in DecimalToRoman)
            {
                while (decimalNumber >= item.Key)
                {
                    romanNumeral += item.Value;
                    decimalNumber -= item.Key;
                }
            }

            return romanNumeral;
        }
    }
}
```

The tests still pass lets now expand the theory test to cover more cases like so... Importantly drive this out one addition test case at a time.

```cs
{
    {
        [Theory]
        [InlineData(1, "I")]
        [InlineData(2, "II")]
        [InlineData(3, "III")]
        [InlineData(4, "IV")]
        [InlineData(5, "V")]
        [InlineData(6, "VI")]
        [InlineData(9, "IX")]
        [InlineData(10, "X")]
        [InlineData(40, "XL")]
        [InlineData(50, "L")]
        [InlineData(90, "XC")]
        [InlineData(100, "C")]
        [InlineData(400, "CD")]
        [InlineData(500, "D")]
        [InlineData(900, "CM")]
        [InlineData(1000, "M")]
        [InlineData(1994, "MCMXCIV")]
        public void ConvertToRomanNumeralReturnsRomanNumeralWhenInputIsDecimal(int numeral, string expectedRomanNumeral)
        {
            // When
            string romanNumeral = romanNumeralConverter.ConvertToRomanNumeral(numeral);

            // Then
            Assert.Equal(expectedRomanNumeral, romanNumeral);
        }
    }
}
```

and the complete solution for the kata is as follows. Due to the generic solution in the refactoring step before simply addition to the dictionary adds all the cases that are needed for the purposes of this solution.

```cs
{
    {
        private readonly Dictionary<int, string> DecimalToRoman = new()
        {
            { 1000, "M" },
            { 900, "CM" },
            { 500, "D" },
            { 400, "CD" },
            { 100, "C" },
            { 90, "XC" },
            { 50, "L" },
            { 40, "XL" },
            { 10, "X" },
            { 9, "IX" },
            { 5, "V" },
            { 4, "IV" },
            { 1, "I" },
        };

        public string ConvertToRomanNumeral(int decimalNumber)
        {
            CheckValidRange(decimalNumber);

            string romanNumeral = string.Empty;

            foreach (var item in DecimalToRoman)
            {
                while (decimalNumber >= item.Key)
                {
                    romanNumeral += item.Value;
                    decimalNumber -= item.Key;
                }
            }

            return romanNumeral;
        }
    }
}
```
