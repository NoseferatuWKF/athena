main.c
```c
int Add(int a, int b) {
    return a + b;
}
```

build shared lib
```bash
gcc -shared -fPIC -o libshared.so main.c
```

Program.cs
>[!warning]
make sure libshared.so is in the dotnet build output
```cs
using System;
using System.Runtime.InteropServices;

class Program
{
    [DllImport("libshared.so", CallingConvention = CallingConvention.Cdecl)]

    private static extern int Add(int a, int b);

    static void Main()
    {
        int result = Add(5, 7);
        Console.WriteLine($"Result from native function: {result}");
    }
}
```