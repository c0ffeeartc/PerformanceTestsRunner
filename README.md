# Performance Tests Runner
Helper scripts to run performance tests and get memory, timing and some other info output in Console

## Usage
  1. Copy `PerformanceTests` folder to your performance tests project
  2. Create test class that implements `IPerformanceTest`, and optionally `IToTestString`
  3. Write `Main` function similar to following:

```csharp
using PerformanceTests;
using R = PerformanceTests.PerformanceTestRunner;

class MainClass
{
    public static void Main(string[] args)
    {
        MemoryHelper.MemoryBegin(  );

        R.run<EmptyTest>("Running performance tests...");

        R.run<EmptyTest>("\nMain tests");
        R.run<Test1>();
        R.run<Test2>();
        R.run( ()=> new TestWithArgs(5,100) );

        R.run<EmptyTest>();
        R.run<EmptyTest>("Other");
        R.run<TestOther1>();
        R.run<TestOther2>();

        MemoryHelper.MemoryEnd(  );
    }
}
```

  4. Run tests and get output similar to:
```
Memory at process start: 4197968, 4447227904, 0, 4447227904, 2568192, 0, 0, 0
Memory before tests: 4215296, 4518735872, 0, 4518735872, 3801088, 0, 0, 0

Running performance tests...

Main Tests
1e+005 Test1:                   116 ms    mem.DIFF 63253056 bytes       mem.ALL 128652168, 4650078208, 0, 4650078208, 138571776, 0, 0, 0 bytes
1e+005 Test2:                   25 ms     mem.DIFF 2889248 bytes        mem.ALL 134854160, 4656947200, 0, 4656947200, 145063936, 0, 0, 0 bytes
1e+005 TestWithArgs:            24 ms     mem.DIFF 2889248 bytes        mem.ALL 132528880, 4684337152, 0, 4684337152, 165433344, 0, 0, 0 bytes

Other
1e+006 TestOther1:              38 ms     mem.DIFF 0 bytes              mem.ALL 57267904, 4583456768, 0, 4583456768, 66060288, 0, 0, 0 bytes
1e+006 TestOther2:              45 ms     mem.DIFF 0 bytes              mem.ALL 57267904, 4583456768, 0, 4583456768, 66060288, 0, 0, 0 bytes

Memory after tests: 58820936, 4585562112, 0, 4585562112, 67633152, 0, 0, 0
```