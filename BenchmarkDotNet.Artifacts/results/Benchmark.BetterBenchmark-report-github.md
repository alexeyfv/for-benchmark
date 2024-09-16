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
| Method               | Runtime  | ItemCount | Mean      | Error    | StdDev    | Gen0   | Code Size | Allocated |
|--------------------- |--------- |---------- |----------:|---------:|----------:|-------:|----------:|----------:|
| For                  | .NET 6.0 | 100000    |  72.35 μs | 0.134 μs |  0.165 μs |      - |      98 B |         - |
| ForEach              | .NET 6.0 | 100000    |  68.80 μs | 0.819 μs |  1.036 μs |      - |     127 B |         - |
| ForEach_Linq         | .NET 6.0 | 100000    | 139.54 μs | 0.260 μs |  0.329 μs |      - |     137 B |         - |
| ForEach_Parallel     | .NET 6.0 | 100000    | 804.11 μs | 8.195 μs | 10.940 μs |      - |     565 B |    5522 B |
| ForEach_LinqParallel | .NET 6.0 | 100000    | 885.41 μs | 8.300 μs | 10.793 μs |      - |     624 B |    7887 B |
| For_Span             | .NET 6.0 | 100000    |  46.34 μs | 0.102 μs |  0.129 μs |      - |     124 B |         - |
| ForEach_Span         | .NET 6.0 | 100000    |  45.63 μs | 0.112 μs |  0.149 μs |      - |        NA |         - |
| For                  | .NET 8.0 | 100000    | 115.38 μs | 0.273 μs |  0.345 μs |      - |      97 B |         - |
| ForEach              | .NET 8.0 | 100000    | 114.89 μs | 0.330 μs |  0.429 μs |      - |        NA |         - |
| ForEach_Linq         | .NET 8.0 | 100000    | 155.29 μs | 2.422 μs |  3.150 μs |      - |     228 B |         - |
| ForEach_Parallel     | .NET 8.0 | 100000    | 494.79 μs | 3.344 μs |  4.349 μs |      - |   1,522 B |    5710 B |
| ForEach_LinqParallel | .NET 8.0 | 100000    | 410.97 μs | 2.792 μs |  3.728 μs | 0.4883 |     460 B |    7891 B |
| For_Span             | .NET 8.0 | 100000    | 114.31 μs | 0.549 μs |  0.654 μs |      - |     117 B |         - |
| ForEach_Span         | .NET 8.0 | 100000    | 113.11 μs | 0.536 μs |  0.716 μs |      - |        NA |         - |
| For                  | .NET 9.0 | 100000    | 115.05 μs | 0.369 μs |  0.480 μs |      - |      95 B |         - |
| ForEach              | .NET 9.0 | 100000    | 114.63 μs | 0.148 μs |  0.197 μs |      - |        NA |         - |
| ForEach_Linq         | .NET 9.0 | 100000    | 154.41 μs | 0.922 μs |  1.198 μs |      - |     227 B |         - |
| ForEach_Parallel     | .NET 9.0 | 100000    | 388.44 μs | 3.457 μs |  4.615 μs |      - |     512 B |    5721 B |
| ForEach_LinqParallel | .NET 9.0 | 100000    | 417.66 μs | 2.848 μs |  3.802 μs | 0.4883 |   1,286 B |    7896 B |
| For_Span             | .NET 9.0 | 100000    |  92.82 μs | 0.334 μs |  0.446 μs |      - |      98 B |         - |
| ForEach_Span         | .NET 9.0 | 100000    |  89.16 μs | 0.547 μs |  0.731 μs |      - |        NA |         - |
