# Outside-In

## Introduction

Outside-in test driven development is the process of developing software from the overarching design architecture to the detail. This test driven approach uses test doubles to check component interactions within a tested unit.

## Design Using Outside-In TDD

In order to design code using outside-in TDD we must ensure we use the same test double reference; we must also make sure that we depend on abstractions rather than concretes through the use of interfaces that can be overriden by mocking libraries.

For this to be the case the object in question must override an interface passed in as a parameter through the constructor or method being tested.

### Example Of Structure Using Constructor Parameters

```cs
public class ExampleClass : IExampleClass
{
    // Private field created that will use the same reference as in the tests
    private readonly IComponentInterface component;

    // Test doubles can override "component" and use the same reference as in the tests
    public ExampleClass(IComponentInterface component)
    {
        this.component = component;
    }

    public void SomeMethod() 
    {
        // Using the same reference we are then able to test this behaviour is executed
        component.SomeActionFromTheComponent();
    }
}
```

### Example Of Structure Using Method Parameters

```cs
public class ExampleClass : IExampleClass
{
    // Test doubles can override "component" and use the same reference
    public void SomeMethod(IComponentInterface component) 
    {
        // Using the same reference we are then able to test this behaviour is executed
        component.SomeActionFromTheComponent();
    }
}
```

### Poor Design

This may at first seem restricting at first however, oop code design principles state to depend upon abstractions.

In the example below "SomeMethod()" is tightly coupled to the "Component" class which means that testing "SomeMethod()" would also be testing "Component" which is also poor test design and an approach that can be often taken (by accident) from doing "Test After Development" (TAD).

In the example below any changes made to how the component class works will have a direct impact on "ExampleClass"

```cs
public class ExampleClass : IExampleClass
{
    public void SomeMethod() 
    {
        // Using the concrete directly couples the behaviour of "Component" to "ExampleClass"
        // This violates the D in SOLID 
        new Component().SomeActionFromTheComponent();
    }
}
```

## Best Practise

* Focus on covering the public interface of each class (public methods)
* Ensure edge case behaviours are covered in the tests by thinking about the ways in which the method can be used and abused through stubbing.
* Ensure components are making expected method calls usings mocks.
* Create fakes for complex external systems (mainly).
* Use a mocking library.

## Example

Outside-in test driven development is best placed when testing component interactions within a unit. The component itself will be tested with inside-out test driven development. This can be demonstrated with the Banking Kata. Follow along with the steps in the example following the red, green, refactor, repeat process.

### Kata

Bank kata. Create a solution for a bank's account service that contains an in data repository that can make deposits, withdraws and print a statement.

Git clone this template <https://github.com/Steelstone3/C-Sharp-Project-Template>

Write a class named Account that implements the following public interface:

```cs
public interface IAccountService
{
    void Deposit(uint amount, DateTime date);
    void Withdraw(uint amount, DateTime date);
    void PrintStatement();
}
```

User interface for taking input is optional. The presentation of the user's statement isn't important to the acceptance criteria. decimal is normally used for currency however for this kata unsigned integers will suffice.

Date | Amount | Balance
| :-- | :--: | :--: |
21/03/2023 | -500 | 2500
13/01/2023 | 2000 | 3000
10/11/2022 | 1000 | 1000

### Steps

Setup the account service starting from the test.

```cs
public class AccountServiceShould
{
    private readonly IAccountService account;

    public AccountServiceShould()
    {
        account = new AccountService();
    }
}

public interface IAccountService
{
    void Deposit(uint amount, DateTime date);
    void Withdraw(uint amount, DateTime date);
    void PrintStatement();
}

public class AcountService : IAccountService
{
    public Deposit(uint amount, DateTime date)
    {
        throw new NotImplemenedException();
    }

    public Withdrawal(uint amount, DateTime date)
    {
        throw new NotImplemenedException();
    }

    public PrintStatement()
    {
        throw new NotImplemenedException();
    }
}
```

Next we are going to need to create an account repository to store the account transactions. We currently don't know how we want account repository to look like just that we want one. It will be used when we make a deposit and withdrawal.

For this we will use Moq to wrap an "IAccountRepository" we will create through the tests.

We will then inject this into the constructor of "AccountService"

```cs
public class AccountServiceShould
{
    private readonly Mock<IAccountRepository> accountRepository = new();
    private readonly IAccountService account;

    public AccountServiceShould()
    {
        account = new AccountService(accountRepository);
    }
}

public interface IAccountRepository 
{

}
```

Now for the first test of the account service (outside). Making a deposit will call account repository's "Deposit()" method that we will create but not implement. We are also not creating a concrete (class) account repository at this moment.

The account repository is passed into the constructor and therefore has the same reference as the test double being used in the test.

```cs
public class AccountServiceShould
{
    ...

    [Fact]
    public void MakeADeposit()
    {
        // Act
        DateTime date = DateTime.Now;
        const uint amount = 500;
        accountRepository.Setup(accountRepo => accountRepo.Deposit(amount, date));
        
        // Arrange
        account.Deposit(amount, date);
        
        // Assert
        accountRepository.VerifyAll();
    }
}

public interface IAccountRepository 
{
    void Deposit(uint amount, DateTime date);
}
```

The make a deposit test checks that the account repository makes its "Deposit()" method call.

Likewise we should do this for withdrawal.

```cs
public class AccountServiceShould
{
    ...

    [Fact]
    public void MakeAWithdrawal()
    {
        // Act
        DateTime date = DateTime.Now;
        const uint amount = 500;
        accountRepository.Setup(ar => ar.Withdraw(amount, date));

        // Arrange
        account.Withdraw(amount, date);

        // Assert
        accountRepository.VerifyAll();
    }
}

public interface IAccountRepository 
{
    void Deposit(uint amount, DateTime date);
    void Withdraw(uint amount, DateTime date);
}
```

Now we can focus on implementing the account repository using inside out.

Start by implementing account repository from the tests.

```cs
public class AccountRepositoryShould
{
    private readonly IAccountRepository accountRepository = new AccountRepository();
}

public class AccountRepository : IAccountRepository
{
    public Deposit(uint amount, DateTime date)
    {
        throw new NotImplemenedException();
    }

    public Withdrawal(uint amount, DateTime date)
    {
        throw new NotImplemenedException();
    }
}
```

Now drive out account repository using the inside-out approach.

Lets start with wrapping transactions (this is an early refactor and normally this would be discovered through the TDD process)

```cs
// This refactor is a few steps ahead in a pure TDD approach
public class TransactionShould
{
    [Fact]
    public void Construct()
    {
        // Arrange
        const int balance = 1000;
        const int amount = -500;
        DateTime dateTime = DateTime.Now;
        ITransaction transaction = new Transaction(dateTime, balance, amount);

        // Assert
        Assert.Equal(dateTime, transaction.Date);
        Assert.Equal(balance, transaction.Balance);
        Assert.Equal(amount, transaction.Amount);
    }
}

public class Transaction : ITransaction
{
    public Transaction(DateTime date, int balance, int amount)
    {
        Date = date;
        Balance = balance;
        Amount = amount;
    }

    public DateTime Date { get; }
    public int Balance { get; }
    public int Amount { get; }    
}
```

Now lets add a list of transactions to the account repository. This will allow the repository to store all of the accounts transactions in data.

```cs
public class AccountRepositoryShould
{
    ...

    [Fact]
    public void Construct()
    {
        // Then
        Assert.NotNull(accountRepository.Transactions);
    }
}

public class AccountRepository : IAccountRepository
{
    public List<ITransaction> Transactions { get; } = new List<ITransaction>();

    ...
}
```

Next we will implement depositing in the account repository. This will use an inside out test approach. Deposits add to the accounts balance.

```cs
// Again this is a few steps ahead in a pure TDD approach
public class AccountRepositoryShould
{
    ...

    [Fact]
    public void MakeADeposit()
    {
        // Arrange
        DateTime date = DateTime.Now;
        const int balance = 500;
        const int amountOutput = 500;
        const uint amountInput = 500;

        // Act
        accountRepository.Deposit(amountInput, date);

        // Assert
        Assert.NotEmpty(accountRepository.Transactions);
        Assert.Equal(balance, accountRepository.Transactions[0].Balance);
        Assert.Equal(amountOutput, accountRepository.Transactions[0].Amount);
        Assert.Equal(date, accountRepository.Transactions[0].Date);
    }
}

public class AccountRepository : IAccountRepository
{
    private int balance;
    public List<ITransaction> Transactions { get; } = new List<ITransaction>();

    public void Deposit(uint amount, DateTime date)
    {
        balance += (int)amount;
        Transaction transaction = new(date, balance, (int)amount);
        Transactions.Add(transaction);
    }

    ...
}
```

We will now implement withdrawals for the account repository.

```cs
public class AccountRepositoryShould
{
    ...

    [Fact]
    public void MakeAWithdrawal()
    {
        // Arrange
        DateTime date = DateTime.Now;
        const int balance = -500;
        const int amountOutput = -500;
        const uint amount = 500;

        // Act
        accountRepository.Withdraw(amount, date);

        // Assert
        Assert.NotEmpty(accountRepository.Transactions);
        Assert.Equal(balance, accountRepository.Transactions[0].Balance);
        Assert.Equal(amountOutput, accountRepository.Transactions[0].Amount);
    }
}

public class AccountRepository : IAccountRepository
{
    ...

    public void Withdraw(uint amount, DateTime date)
    {
        balance -= (int)amount;
        Transaction transaction = new(date, balance, -(int)amount);
        Transactions.Add(transaction);
    }
}
```

Lastly for the account repository it can be a good idea to write an acceptance test which will test an expected path in how a component will be used.

```cs
public class AccountRepositoryShould
{
    ...

    [Fact]
    public void Acceptance()
    {
        // Arrange
        DateTime date = DateTime.Now;
        const uint amount = 500;

        // Act
        accountRepository.Deposit(amount, date);
        accountRepository.Deposit(amount, date);
        accountRepository.Deposit(250, date);
        accountRepository.Withdraw(amount, date);

        // Assert
        Assert.NotEmpty(accountRepository.Transactions);
        Assert.Equal(500, accountRepository.Transactions[0].Balance);
        Assert.Equal(500, accountRepository.Transactions[0].Amount);
        Assert.Equal(date, accountRepository.Transactions[0].Date);
        Assert.Equal(1000, accountRepository.Transactions[1].Balance);
        Assert.Equal(500, accountRepository.Transactions[1].Amount);
        Assert.Equal(date, accountRepository.Transactions[1].Date);
        Assert.Equal(1250, accountRepository.Transactions[2].Balance);
        Assert.Equal(250, accountRepository.Transactions[2].Amount);
        Assert.Equal(date, accountRepository.Transactions[2].Date);
        Assert.Equal(750, accountRepository.Transactions[3].Balance);
        Assert.Equal(-500, accountRepository.Transactions[3].Amount);
        Assert.Equal(date, accountRepository.Transactions[3].Date);
    }
}
```

Normally a unit test has one act to track one change. Acceptance tests meanwhile can be used to test a path through a program.

We now have a program that has an implemented repository. We now need a means to print the output.

For this we will pass a "IStatementPrinter" into the "PrintStatement()" function of the "AccountService".

```cs
public class AccountServiceShould
{
    ...

    [Fact]
    public void PrintAStatement()
    {
        // Act
        statementPrinter.Setup(sp => sp.PrintStatement(accountRepository.Object.Transactions));

        // Arrange
        account.PrintStatement(statementPrinter.Object);

        // Assert
        statementPrinter.VerifyAll();
    }
}

public class AccountService : IAccountService
{
    ...

    public void PrintStatement(IStatementPrinter statementPrinter)
    {
        statementPrinter.PrintStatement(accountRepository.Transactions);
    }
}
```

This test checks that "PrintStatement()" is called by the "StatementPrinter"

The statement printer itself can now be implemented. In this case we have two options. On the one hand we can wrap "System.Console.WriteLine()" and mock this to determine the statement printer works as intended. Alternatively we can use a third party console interface to print a table of the statement which this example shows.

Realisitically most user interfaces can't utalise test doubles so can't be tested with unit or acceptance tests and would typically fall under automated user interface testing such as through the usage of tools such as cypress.

```cs
public class StatementPrinter : IStatementPrinter
{
    public void PrintStatement(IEnumerable<ITransaction> transactions)
    {
        Table table = CreateTable();
        WriteRows(transactions, table);
        AnsiConsole.Write(table);
    }

    private static Table CreateTable()
    {
        Table table = new()
        {
            Title = new TableTitle("Account")
        };

        table.AddColumn("Date");
        table.AddColumn("Amount");
        table.AddColumn("Balance");

        return table;
    }

    private static void WriteRows(IEnumerable<ITransaction> transactions, Table table)
    {
        // Reverse for loop (forr)
        for (int i = transactions.Count() - 1; i >= 0; i--)
        {
            table.AddRow($"{transactions.ToArray()[i].Date}", $"{transactions.ToArray()[i].Amount}", $"{transactions.ToArray()[i].Balance}");
        }
    }
}
```

Lets quickly implement what we have created so far

```cs
internal static class Program
{
    internal static void Main()
    {
        AccountService account = new(new AccountRepository());
        account.Deposit(500, DateTime.Now);
        account.Deposit(1000, DateTime.Now);
        account.Withdraw(250, DateTime.Now);
        account.PrintStatement(new StatementPrinter());
    }
}
```

Acceptance criteria has been met and this will create the following approximate output.

Date | Amount | Balance
| :-- | :--: | :--: |
21/03/2023 | -500 | 2500
13/01/2023 | 2000 | 3000
10/11/2022 | 1000 | 1000
