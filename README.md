### THREADING(*Basics of Multi-Threading and how to handle Race Conditions*)

*Example*

```csharp
using System;
using System.Threading;

class Program
{
    static int total = 0;
    // CREATE NEW LOCK OBJECT INSTANCE
    static readonly object lockObject = new();

    static void Main()
    {
        Thread thread1 = new(IncrementTotal);
        Thread thread2 = new(IncrementTotal);

        thread1.Start();
        thread2.Start();

        thread1.Join();
        thread2.Join();

        Console.WriteLine($"Total: {total}");
    }

    static void IncrementTotal()
    {
        for (int i = 0; i < 100000; i++)
        {
            // ACQUIRE lock BEFORE ACCESSING THE SHARED RESOURCE
            lock (lockObject)
            {
                total++;
            }
        }
    }
}
```
