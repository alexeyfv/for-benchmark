```

BenchmarkDotNet v0.14.0, Windows 10 (10.0.19045.4780/22H2/2022Update)
12th Gen Intel Core i7-12800H, 1 CPU, 20 logical and 14 physical cores
.NET SDK 9.0.100-rc.1.24452.12
  [Host]     : .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
  Job-JFIAZA : .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
  Job-JTKYHY : .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
  Job-MCYVQZ : .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2

IterationCount=25  

```
| Method               | Runtime  | ItemCount | Mean      | Error    | StdDev    | Median    | Gen0   | Allocated |
|--------------------- |--------- |---------- |----------:|---------:|----------:|----------:|-------:|----------:|
| For                  | .NET 6.0 | 100000    |  31.76 μs | 0.138 μs |  0.174 μs |  31.73 μs |      - |         - |
| ForEach              | .NET 6.0 | 100000    |  43.46 μs | 0.286 μs |  0.351 μs |  43.31 μs |      - |         - |
| ForEach_Linq         | .NET 6.0 | 100000    | 136.79 μs | 0.666 μs |  0.866 μs | 136.77 μs |      - |      64 B |
| ForEach_Parallel     | .NET 6.0 | 100000    |  66.44 μs | 1.012 μs |  1.316 μs |  66.56 μs | 0.3662 |    5620 B |
| ForEach_LinqParallel | .NET 6.0 | 100000    | 161.97 μs | 8.138 μs | 10.864 μs | 158.88 μs | 0.4883 |    7960 B |
| For_Span             | .NET 6.0 | 100000    |  29.26 μs | 0.022 μs |  0.027 μs |  29.25 μs |      - |         - |
| ForEach_Span         | .NET 6.0 | 100000    |  29.32 μs | 0.045 μs |  0.057 μs |  29.32 μs |      - |         - |
| For                  | .NET 8.0 | 100000    |  31.55 μs | 0.036 μs |  0.044 μs |  31.54 μs |      - |         - |
| ForEach              | .NET 8.0 | 100000    |  21.14 μs | 0.024 μs |  0.032 μs |  21.14 μs |      - |         - |
| ForEach_Linq         | .NET 8.0 | 100000    |  31.96 μs | 0.309 μs |  0.368 μs |  31.84 μs |      - |      64 B |
| ForEach_Parallel     | .NET 8.0 | 100000    |  44.39 μs | 0.222 μs |  0.289 μs |  44.30 μs | 0.4272 |    5745 B |
| ForEach_LinqParallel | .NET 8.0 | 100000    |  54.23 μs | 0.340 μs |  0.405 μs |  54.18 μs | 0.6104 |    7960 B |
| For_Span             | .NET 8.0 | 100000    |  21.40 μs | 0.085 μs |  0.114 μs |  21.41 μs |      - |         - |
| ForEach_Span         | .NET 8.0 | 100000    |  21.66 μs | 0.634 μs |  0.846 μs |  21.16 μs |      - |         - |
| For                  | .NET 9.0 | 100000    |  31.52 μs | 0.022 μs |  0.029 μs |  31.52 μs |      - |         - |
| ForEach              | .NET 9.0 | 100000    |  21.04 μs | 0.016 μs |  0.020 μs |  21.03 μs |      - |         - |
| ForEach_Linq         | .NET 9.0 | 100000    |  31.64 μs | 0.048 μs |  0.061 μs |  31.62 μs |      - |      64 B |
| ForEach_Parallel     | .NET 9.0 | 100000    |  43.89 μs | 0.265 μs |  0.353 μs |  43.82 μs | 0.4272 |    5791 B |
| ForEach_LinqParallel | .NET 9.0 | 100000    |  44.63 μs | 0.121 μs |  0.152 μs |  44.65 μs | 0.6104 |    7958 B |
| For_Span             | .NET 9.0 | 100000    |  21.04 μs | 0.017 μs |  0.021 μs |  21.03 μs |      - |         - |
| ForEach_Span         | .NET 9.0 | 100000    |  21.03 μs | 0.010 μs |  0.012 μs |  21.03 μs |      - |         - |
