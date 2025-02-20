# Asynchronous Programming

## Introduction

Asynchronous programming is a means of providing non-blocking code-execution to the main program thread.

The best types of usecases for asynchronous programming is when waiting on an external source to the program such as a database, website server and so on.

## How It Works

Running code provides the CPU something known as a task queue. In synchronous programming this queue (stored cache) is ran in order when resource becomes avaliable in the CPU.

Asynchronous programming allows for a task to sit outside of the queue and performs polling on the CPU to when resource becomes avaliable in the CPU where it can slot in to execute in a non-blocking way. Therefore asynchronous execution is performed in a synchronous execution when resource is avaliable. As developers therefore the consideration is the performance overhead of asynchronous programming and whether it is required.

Importantly UI libraries are typically ran on a UI thread therefore don't require non-blocking programming practises (asynchronous).

### Promises

In software a promise is an object that represent the eventual result of an asynchronous operation.

Promises can have the following states

- Pending
- Fulfilled
- Rejected

For C# a task acts as the wrapper to provide the promise

## Code Example

In C# to run code asynchronously use the keywords async and await with the non-blocking execution returning Task

Split the blocking code off into a method that returns Task

```cs
public async void GetStockLevels()
{
    // synchronous call to get the query
    string query = GetQuery();

    // asynchronous call to connect to the database
    await ConnectToDatabase();

    // asynchronous call to call the database
    List<Stock> stocks = await GetStocksFromDatabase(query);

    // synchronous call to display stock in UI
    DisplayStocksLoadDialog(stocks)
}

private Task ConnectToDatabase() {
    
}

private Task<List<Stock>> GetStocksFromDatabase(string query) {
    return new List<Stock>() {...}
}
```

Important note the
