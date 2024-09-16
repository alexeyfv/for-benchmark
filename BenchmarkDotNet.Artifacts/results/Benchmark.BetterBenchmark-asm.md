## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
       7FFD4C298180 push      rdi
       7FFD4C298181 push      rsi
       7FFD4C298182 push      rbx
       7FFD4C298183 sub       rsp,20
       7FFD4C298187 mov       rsi,rcx
;         sum = 0;
;         ^^^^^^^^
       7FFD4C29818A mov       dword ptr [7FFD4C22ECA0],0
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
       7FFD4C298194 xor       edi,edi
       7FFD4C298196 mov       rbx,[rsi+8]
       7FFD4C29819A cmp       dword ptr [rbx+10],0
       7FFD4C29819E jle       short M00_L01
;             sum += DoSomething(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L00:
       7FFD4C2981A0 mov       ebx,[7FFD4C22ECA0]
       7FFD4C2981A6 mov       rcx,[rsi+8]
       7FFD4C2981AA cmp       edi,[rcx+10]
       7FFD4C2981AD jae       short M00_L02
       7FFD4C2981AF mov       rcx,[rcx+8]
       7FFD4C2981B3 cmp       edi,[rcx+8]
       7FFD4C2981B6 jae       short M00_L03
       7FFD4C2981B8 movsxd    rax,edi
       7FFD4C2981BB mov       ecx,[rcx+rax*4+10]
       7FFD4C2981BF call      Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD4C2981C4 add       eax,ebx
       7FFD4C2981C6 mov       [7FFD4C22ECA0],eax
       7FFD4C2981CC inc       edi
       7FFD4C2981CE mov       rbx,[rsi+8]
       7FFD4C2981D2 cmp       edi,[rbx+10]
       7FFD4C2981D5 jl        short M00_L00
;         return sum;
;         ^^^^^^^^^^^
M00_L01:
       7FFD4C2981D7 mov       eax,[7FFD4C22ECA0]
       7FFD4C2981DD add       rsp,20
       7FFD4C2981E1 pop       rbx
       7FFD4C2981E2 pop       rsi
       7FFD4C2981E3 pop       rdi
       7FFD4C2981E4 ret
M00_L02:
       7FFD4C2981E5 call      System.ThrowHelper.ThrowArgumentOutOfRange_IndexException()
       7FFD4C2981EA int       3
M00_L03:
       7FFD4C2981EB call      CORINFO_HELP_RNGCHKFAIL
       7FFD4C2981F0 int       3
; Total bytes of code 113
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD4C2B2C80 lea       eax,[rcx+rcx]
       7FFD4C2B2C83 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowArgumentOutOfRange_IndexException()

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach()
       7FFD4C2A8F20 push      rdi
       7FFD4C2A8F21 push      rsi
       7FFD4C2A8F22 push      rbp
       7FFD4C2A8F23 push      rbx
       7FFD4C2A8F24 sub       rsp,28
;         sum = 0;
;         ^^^^^^^^
       7FFD4C2A8F28 mov       dword ptr [7FFD4C23ECA0],0
;         foreach (var item in List)
;                              ^^^^
       7FFD4C2A8F32 mov       rsi,[rcx+8]
       7FFD4C2A8F36 mov       edi,[rsi+14]
       7FFD4C2A8F39 xor       ebx,ebx
       7FFD4C2A8F3B jmp       short M00_L01
;             sum += DoSomething(item);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L00:
       7FFD4C2A8F3D mov       ebp,[7FFD4C23ECA0]
       7FFD4C2A8F43 call      Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD4C2A8F48 add       eax,ebp
       7FFD4C2A8F4A mov       [7FFD4C23ECA0],eax
M00_L01:
       7FFD4C2A8F50 mov       rcx,rsi
       7FFD4C2A8F53 cmp       edi,[rcx+14]
       7FFD4C2A8F56 jne       short M00_L02
       7FFD4C2A8F58 cmp       ebx,[rsi+10]
       7FFD4C2A8F5B jae       short M00_L03
       7FFD4C2A8F5D mov       rcx,[rsi+8]
       7FFD4C2A8F61 cmp       ebx,[rcx+8]
       7FFD4C2A8F64 jae       short M00_L06
       7FFD4C2A8F66 movsxd    rax,ebx
       7FFD4C2A8F69 mov       ecx,[rcx+rax*4+10]
       7FFD4C2A8F6D inc       ebx
       7FFD4C2A8F6F mov       eax,1
       7FFD4C2A8F74 jmp       short M00_L04
M00_L02:
       7FFD4C2A8F76 cmp       edi,[rsi+14]
       7FFD4C2A8F79 jne       short M00_L05
M00_L03:
       7FFD4C2A8F7B mov       ebx,[rsi+10]
       7FFD4C2A8F7E inc       ebx
       7FFD4C2A8F80 xor       ecx,ecx
       7FFD4C2A8F82 xor       eax,eax
M00_L04:
       7FFD4C2A8F84 test      eax,eax
       7FFD4C2A8F86 jne       short M00_L00
;         return sum;
;         ^^^^^^^^^^^
       7FFD4C2A8F88 mov       eax,[7FFD4C23ECA0]
       7FFD4C2A8F8E add       rsp,28
       7FFD4C2A8F92 pop       rbx
       7FFD4C2A8F93 pop       rbp
       7FFD4C2A8F94 pop       rsi
       7FFD4C2A8F95 pop       rdi
       7FFD4C2A8F96 ret
M00_L05:
       7FFD4C2A8F97 call      System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()
       7FFD4C2A8F9C int       3
M00_L06:
       7FFD4C2A8F9D call      CORINFO_HELP_RNGCHKFAIL
       7FFD4C2A8FA2 int       3
; Total bytes of code 131
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD4C2C2D80 lea       eax,[rcx+rcx]
       7FFD4C2C2D83 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         sum = 0;
;         ^^^^^^^^
;         List.ForEach(_doSomething);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD4C2B2DE0 sub       rsp,28
       7FFD4C2B2DE4 mov       dword ptr [7FFD4C22ECA0],0
       7FFD4C2B2DEE mov       [rsp+30],rcx
       7FFD4C2B2DF3 mov       rcx,[rcx+8]
       7FFD4C2B2DF7 mov       rdx,[rsp+30]
       7FFD4C2B2DFC mov       rdx,[rdx+10]
       7FFD4C2B2E00 cmp       [rcx],ecx
       7FFD4C2B2E02 call      System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD4C2B2E07 mov       eax,[7FFD4C22ECA0]
       7FFD4C2B2E0D add       rsp,28
       7FFD4C2B2E11 ret
; Total bytes of code 50
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD4C2B2E40 push      rdi
       7FFD4C2B2E41 push      rsi
       7FFD4C2B2E42 push      rbp
       7FFD4C2B2E43 push      rbx
       7FFD4C2B2E44 sub       rsp,28
       7FFD4C2B2E48 mov       rsi,rcx
       7FFD4C2B2E4B mov       rdi,rdx
       7FFD4C2B2E4E test      rdi,rdi
       7FFD4C2B2E51 je        short M01_L02
       7FFD4C2B2E53 mov       ebx,[rsi+14]
       7FFD4C2B2E56 xor       ebp,ebp
       7FFD4C2B2E58 cmp       dword ptr [rsi+10],0
       7FFD4C2B2E5C jle       short M01_L01
M01_L00:
       7FFD4C2B2E5E cmp       ebx,[rsi+14]
       7FFD4C2B2E61 jne       short M01_L01
       7FFD4C2B2E63 mov       rcx,[rsi+8]
       7FFD4C2B2E67 cmp       ebp,[rcx+8]
       7FFD4C2B2E6A jae       short M01_L04
       7FFD4C2B2E6C movsxd    rdx,ebp
       7FFD4C2B2E6F mov       edx,[rcx+rdx*4+10]
       7FFD4C2B2E73 mov       rax,rdi
       7FFD4C2B2E76 mov       rcx,[rax+8]
       7FFD4C2B2E7A call      qword ptr [rax+18]
       7FFD4C2B2E7D inc       ebp
       7FFD4C2B2E7F cmp       ebp,[rsi+10]
       7FFD4C2B2E82 jl        short M01_L00
M01_L01:
       7FFD4C2B2E84 cmp       ebx,[rsi+14]
       7FFD4C2B2E87 jne       short M01_L03
       7FFD4C2B2E89 add       rsp,28
       7FFD4C2B2E8D pop       rbx
       7FFD4C2B2E8E pop       rbp
       7FFD4C2B2E8F pop       rsi
       7FFD4C2B2E90 pop       rdi
       7FFD4C2B2E91 ret
M01_L02:
       7FFD4C2B2E92 mov       ecx,1C
       7FFD4C2B2E97 call      System.ThrowHelper.ThrowArgumentNullException(System.ExceptionArgument)
       7FFD4C2B2E9C int       3
M01_L03:
       7FFD4C2B2E9D call      System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()
       7FFD4C2B2EA2 int       3
M01_L04:
       7FFD4C2B2EA3 call      CORINFO_HELP_RNGCHKFAIL
       7FFD4C2B2EA8 int       3
; Total bytes of code 105
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         sum = 0;
;         ^^^^^^^^
;         Parallel.ForEach(List, _doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD4C2E7E00 sub       rsp,38
       7FFD4C2E7E04 mov       dword ptr [7FFD4C25ECA0],0
       7FFD4C2E7E0E mov       rdx,[rcx+8]
       7FFD4C2E7E12 mov       r8,[rcx+18]
       7FFD4C2E7E16 lea       rcx,[rsp+20]
       7FFD4C2E7E1B call      System.Threading.Tasks.Parallel.ForEach[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Action`1<Int32>)
       7FFD4C2E7E20 mov       eax,[7FFD4C25ECA0]
       7FFD4C2E7E26 add       rsp,38
       7FFD4C2E7E2A ret
; Total bytes of code 43
```
```assembly
; System.Threading.Tasks.Parallel.ForEach[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Action`1<Int32>)
       7FFD4C2E7E40 push      rbp
       7FFD4C2E7E41 push      r14
       7FFD4C2E7E43 push      rdi
       7FFD4C2E7E44 push      rsi
       7FFD4C2E7E45 push      rbx
       7FFD4C2E7E46 sub       rsp,80
       7FFD4C2E7E4D vzeroupper
       7FFD4C2E7E50 lea       rbp,[rsp+0A0]
       7FFD4C2E7E58 xor       eax,eax
       7FFD4C2E7E5A mov       [rbp-40],rax
       7FFD4C2E7E5E mov       rbx,rcx
       7FFD4C2E7E61 mov       rsi,rdx
       7FFD4C2E7E64 mov       rdi,r8
       7FFD4C2E7E67 test      rsi,rsi
       7FFD4C2E7E6A je        near ptr M01_L05
       7FFD4C2E7E70 test      rdi,rdi
       7FFD4C2E7E73 je        near ptr M01_L06
       7FFD4C2E7E79 mov       rdx,1B66BEF81C0
       7FFD4C2E7E83 mov       r14,[rdx]
       7FFD4C2E7E86 mov       rdx,[r14+18]
       7FFD4C2E7E8A mov       [rbp-40],rdx
       7FFD4C2E7E8E cmp       qword ptr [rbp-40],0
       7FFD4C2E7E93 jne       near ptr M01_L02
M01_L00:
       7FFD4C2E7E99 mov       rdx,rsi
       7FFD4C2E7E9C mov       rcx,offset MT_System.Int32[]
       7FFD4C2E7EA6 call      CORINFO_HELP_ISINSTANCEOFARRAY
       7FFD4C2E7EAB test      rax,rax
       7FFD4C2E7EAE je        near ptr M01_L03
       7FFD4C2E7EB4 mov       [rsp+20],rdi
       7FFD4C2E7EB9 xor       ecx,ecx
       7FFD4C2E7EBB mov       [rsp+28],rcx
       7FFD4C2E7EC0 mov       [rsp+30],rcx
       7FFD4C2E7EC5 mov       [rsp+38],rcx
       7FFD4C2E7ECA mov       [rsp+40],rcx
       7FFD4C2E7ECF mov       [rsp+48],rcx
       7FFD4C2E7ED4 mov       [rsp+50],rcx
       7FFD4C2E7ED9 lea       rcx,[rbp-38]
       7FFD4C2E7EDD mov       r8,rax
       7FFD4C2E7EE0 mov       r9,r14
       7FFD4C2E7EE3 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD4C2E7EED call      System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M01_L01:
       7FFD4C2E7EF2 vmovdqu   xmm0,xmmword ptr [rbp-38]
       7FFD4C2E7EF7 vmovdqu   xmmword ptr [rbx],xmm0
       7FFD4C2E7EFB mov       rax,[rbp-28]
       7FFD4C2E7EFF mov       [rbx+10],rax
       7FFD4C2E7F03 mov       rax,rbx
       7FFD4C2E7F06 add       rsp,80
       7FFD4C2E7F0D pop       rbx
       7FFD4C2E7F0E pop       rsi
       7FFD4C2E7F0F pop       rdi
       7FFD4C2E7F10 pop       r14
       7FFD4C2E7F12 pop       rbp
       7FFD4C2E7F13 ret
M01_L02:
       7FFD4C2E7F14 mov       rdx,[rbp-40]
       7FFD4C2E7F18 cmp       dword ptr [rdx+20],0
       7FFD4C2E7F1C setne     dl
       7FFD4C2E7F1F movzx     edx,dl
       7FFD4C2E7F22 test      edx,edx
       7FFD4C2E7F24 je        near ptr M01_L00
       7FFD4C2E7F2A jmp       near ptr M01_L07
M01_L03:
       7FFD4C2E7F2F mov       rdx,rsi
       7FFD4C2E7F32 mov       rcx,offset MT_System.Collections.Generic.IList`1[[System.Int32, System.Private.CoreLib]]
       7FFD4C2E7F3C call      CORINFO_HELP_ISINSTANCEOFINTERFACE
       7FFD4C2E7F41 test      rax,rax
       7FFD4C2E7F44 je        short M01_L04
       7FFD4C2E7F46 mov       [rsp+20],rdi
       7FFD4C2E7F4B xor       ecx,ecx
       7FFD4C2E7F4D mov       [rsp+28],rcx
       7FFD4C2E7F52 mov       [rsp+30],rcx
       7FFD4C2E7F57 mov       [rsp+38],rcx
       7FFD4C2E7F5C mov       [rsp+40],rcx
       7FFD4C2E7F61 mov       [rsp+48],rcx
       7FFD4C2E7F66 mov       [rsp+50],rcx
       7FFD4C2E7F6B lea       rcx,[rbp-38]
       7FFD4C2E7F6F mov       r8,rax
       7FFD4C2E7F72 mov       r9,r14
       7FFD4C2E7F75 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD4C2E7F7F call      System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFD4C2E7F84 jmp       near ptr M01_L01
M01_L04:
       7FFD4C2E7F89 mov       rcx,rsi
       7FFD4C2E7F8C xor       edx,edx
       7FFD4C2E7F8E call      System.Collections.Concurrent.Partitioner.Create[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Collections.Concurrent.EnumerablePartitionerOptions)
       7FFD4C2E7F93 mov       r8,rax
       7FFD4C2E7F96 mov       [rsp+20],rdi
       7FFD4C2E7F9B xor       ecx,ecx
       7FFD4C2E7F9D mov       [rsp+28],rcx
       7FFD4C2E7FA2 mov       [rsp+30],rcx
       7FFD4C2E7FA7 mov       [rsp+38],rcx
       7FFD4C2E7FAC mov       [rsp+40],rcx
       7FFD4C2E7FB1 mov       [rsp+48],rcx
       7FFD4C2E7FB6 mov       [rsp+50],rcx
       7FFD4C2E7FBB lea       rcx,[rbp-38]
       7FFD4C2E7FBF mov       r9,r14
       7FFD4C2E7FC2 mov       rdx,offset MD_System.Threading.Tasks.Parallel.PartitionerForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Concurrent.Partitioner`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD4C2E7FCC call      System.Threading.Tasks.Parallel.PartitionerForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Concurrent.Partitioner`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFD4C2E7FD1 jmp       near ptr M01_L01
M01_L05:
       7FFD4C2E7FD6 mov       rcx,offset MT_System.ArgumentNullException
       7FFD4C2E7FE0 call      CORINFO_HELP_NEWSFAST
       7FFD4C2E7FE5 mov       rsi,rax
       7FFD4C2E7FE8 mov       ecx,3C3
       7FFD4C2E7FED mov       rdx,7FFD4C3DEED0
       7FFD4C2E7FF7 call      CORINFO_HELP_STRCNS
       7FFD4C2E7FFC mov       rdx,rax
       7FFD4C2E7FFF mov       rcx,rsi
       7FFD4C2E8002 call      System.ArgumentNullException..ctor(System.String)
       7FFD4C2E8007 mov       rcx,rsi
       7FFD4C2E800A call      CORINFO_HELP_THROW
M01_L06:
       7FFD4C2E800F mov       rcx,offset MT_System.ArgumentNullException
       7FFD4C2E8019 call      CORINFO_HELP_NEWSFAST
       7FFD4C2E801E mov       rsi,rax
       7FFD4C2E8021 mov       ecx,38B
       7FFD4C2E8026 mov       rdx,7FFD4C3DEED0
       7FFD4C2E8030 call      CORINFO_HELP_STRCNS
       7FFD4C2E8035 mov       rdx,rax
       7FFD4C2E8038 mov       rcx,rsi
       7FFD4C2E803B call      System.ArgumentNullException..ctor(System.String)
       7FFD4C2E8040 mov       rcx,rsi
       7FFD4C2E8043 call      CORINFO_HELP_THROW
M01_L07:
       7FFD4C2E8048 lea       rcx,[rbp-40]
       7FFD4C2E804C call      System.Threading.CancellationToken.ThrowOperationCanceledException()
       7FFD4C2E8051 int       3
; Total bytes of code 530
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         sum = 0;
;         ^^^^^^^^
;         List.AsParallel().ForAll(_doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD4C2C9B80 push      rsi
       7FFD4C2C9B81 sub       rsp,20
       7FFD4C2C9B85 mov       rsi,rcx
       7FFD4C2C9B88 mov       dword ptr [7FFD4C23ECA0],0
       7FFD4C2C9B92 mov       rcx,[rsi+8]
       7FFD4C2C9B96 call      System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD4C2C9B9B mov       rcx,rax
       7FFD4C2C9B9E mov       rdx,[rsi+18]
       7FFD4C2C9BA2 call      System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFD4C2C9BA7 mov       eax,[7FFD4C23ECA0]
       7FFD4C2C9BAD add       rsp,20
       7FFD4C2C9BB1 pop       rsi
       7FFD4C2C9BB2 ret
; Total bytes of code 51
```
```assembly
; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD4C2C9BD0 push      rdi
       7FFD4C2C9BD1 push      rsi
       7FFD4C2C9BD2 push      rbp
       7FFD4C2C9BD3 push      rbx
       7FFD4C2C9BD4 sub       rsp,88
       7FFD4C2C9BDB vzeroupper
       7FFD4C2C9BDE xor       eax,eax
       7FFD4C2C9BE0 mov       [rsp+28],rax
       7FFD4C2C9BE5 vxorps    xmm4,xmm4,xmm4
       7FFD4C2C9BE9 vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFD4C2C9BEF vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFD4C2C9BF5 vmovdqa   xmmword ptr [rsp+50],xmm4
       7FFD4C2C9BFB vmovdqa   xmmword ptr [rsp+60],xmm4
       7FFD4C2C9C01 vmovdqa   xmmword ptr [rsp+70],xmm4
       7FFD4C2C9C07 mov       [rsp+80],rax
       7FFD4C2C9C0F mov       rbx,rcx
       7FFD4C2C9C12 test      rbx,rbx
       7FFD4C2C9C15 je        near ptr M01_L00
       7FFD4C2C9C1B mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD4C2C9C25 call      CORINFO_HELP_NEWSFAST
       7FFD4C2C9C2A mov       rbp,rax
       7FFD4C2C9C2D lea       rcx,[rsp+58]
       7FFD4C2C9C32 call      System.Linq.Parallel.QuerySettings.get_Empty()
       7FFD4C2C9C37 vmovdqu   xmm0,xmmword ptr [rsp+58]
       7FFD4C2C9C3D vmovdqu   xmmword ptr [rsp+28],xmm0
       7FFD4C2C9C43 vmovdqu   xmm0,xmmword ptr [rsp+68]
       7FFD4C2C9C49 vmovdqu   xmmword ptr [rsp+38],xmm0
       7FFD4C2C9C4F vmovdqu   xmm0,xmmword ptr [rsp+78]
       7FFD4C2C9C55 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFD4C2C9C5B lea       rdi,[rbp+8]
       7FFD4C2C9C5F lea       rsi,[rsp+28]
       7FFD4C2C9C64 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD4C2C9C69 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD4C2C9C6E mov       ecx,4
       7FFD4C2C9C73 rep movsq
       7FFD4C2C9C76 lea       rcx,[rbp+38]
       7FFD4C2C9C7A mov       rdx,rbx
       7FFD4C2C9C7D call      CORINFO_HELP_ASSIGN_REF
       7FFD4C2C9C82 mov       rax,rbp
       7FFD4C2C9C85 add       rsp,88
       7FFD4C2C9C8C pop       rbx
       7FFD4C2C9C8D pop       rbp
       7FFD4C2C9C8E pop       rsi
       7FFD4C2C9C8F pop       rdi
       7FFD4C2C9C90 ret
M01_L00:
       7FFD4C2C9C91 mov       rcx,offset MT_System.ArgumentNullException
       7FFD4C2C9C9B call      CORINFO_HELP_NEWSFAST
       7FFD4C2C9CA0 mov       rsi,rax
       7FFD4C2C9CA3 mov       ecx,6F1
       7FFD4C2C9CA8 mov       rdx,7FFD4C3791D8
       7FFD4C2C9CB2 call      CORINFO_HELP_STRCNS
       7FFD4C2C9CB7 mov       rdx,rax
       7FFD4C2C9CBA mov       rcx,rsi
       7FFD4C2C9CBD call      System.ArgumentNullException..ctor(System.String)
       7FFD4C2C9CC2 mov       rcx,rsi
       7FFD4C2C9CC5 call      CORINFO_HELP_THROW
       7FFD4C2C9CCA int       3
; Total bytes of code 251
```
```assembly
; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFD4C2CA1E0 push      r15
       7FFD4C2CA1E2 push      r14
       7FFD4C2CA1E4 push      rdi
       7FFD4C2CA1E5 push      rsi
       7FFD4C2CA1E6 push      rbp
       7FFD4C2CA1E7 push      rbx
       7FFD4C2CA1E8 sub       rsp,58
       7FFD4C2CA1EC vzeroupper
       7FFD4C2CA1EF xor       eax,eax
       7FFD4C2CA1F1 mov       [rsp+28],rax
       7FFD4C2CA1F6 vxorps    xmm4,xmm4,xmm4
       7FFD4C2CA1FA vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFD4C2CA200 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFD4C2CA206 mov       [rsp+50],rax
       7FFD4C2CA20B mov       rsi,rcx
       7FFD4C2CA20E mov       rbx,rdx
       7FFD4C2CA211 test      rsi,rsi
       7FFD4C2CA214 je        near ptr M02_L00
       7FFD4C2CA21A test      rbx,rbx
       7FFD4C2CA21D je        near ptr M02_L01
       7FFD4C2CA223 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFD4C2CA22D call      CORINFO_HELP_NEWSFAST
       7FFD4C2CA232 mov       rbp,rax
       7FFD4C2CA235 mov       rcx,rsi
       7FFD4C2CA238 call      System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD4C2CA23D mov       r14,rax
       7FFD4C2CA240 movzx     ecx,byte ptr [r14+38]
       7FFD4C2CA245 vmovdqu   xmm0,xmmword ptr [r14+8]
       7FFD4C2CA24B vmovdqu   xmmword ptr [rsp+28],xmm0
       7FFD4C2CA251 vmovdqu   xmm0,xmmword ptr [r14+18]
       7FFD4C2CA257 vmovdqu   xmmword ptr [rsp+38],xmm0
       7FFD4C2CA25D vmovdqu   xmm0,xmmword ptr [r14+28]
       7FFD4C2CA263 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFD4C2CA269 movzx     r15d,cl
       7FFD4C2CA26D mov       byte ptr [rbp+48],3
       7FFD4C2CA271 lea       rdi,[rbp+8]
       7FFD4C2CA275 lea       rsi,[rsp+28]
       7FFD4C2CA27A call      CORINFO_HELP_ASSIGN_BYREF
       7FFD4C2CA27F call      CORINFO_HELP_ASSIGN_BYREF
       7FFD4C2CA284 mov       ecx,4
       7FFD4C2CA289 rep movsq
       7FFD4C2CA28C mov       [rbp+38],r15b
       7FFD4C2CA290 lea       rcx,[rbp+40]
       7FFD4C2CA294 mov       rdx,r14
       7FFD4C2CA297 call      CORINFO_HELP_ASSIGN_REF
       7FFD4C2CA29C lea       rcx,[rbp+50]
       7FFD4C2CA2A0 mov       rdx,rbx
       7FFD4C2CA2A3 call      CORINFO_HELP_ASSIGN_REF
       7FFD4C2CA2A8 mov       rcx,rbp
       7FFD4C2CA2AB add       rsp,58
       7FFD4C2CA2AF pop       rbx
       7FFD4C2CA2B0 pop       rbp
       7FFD4C2CA2B1 pop       rsi
       7FFD4C2CA2B2 pop       rdi
       7FFD4C2CA2B3 pop       r14
       7FFD4C2CA2B5 pop       r15
       7FFD4C2CA2B7 jmp       near ptr System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
M02_L00:
       7FFD4C2CA2BC mov       rcx,offset MT_System.ArgumentNullException
       7FFD4C2CA2C6 call      CORINFO_HELP_NEWSFAST
       7FFD4C2CA2CB mov       rsi,rax
       7FFD4C2CA2CE mov       ecx,6F1
       7FFD4C2CA2D3 mov       rdx,7FFD4C3791D8
       7FFD4C2CA2DD call      CORINFO_HELP_STRCNS
       7FFD4C2CA2E2 mov       rdx,rax
       7FFD4C2CA2E5 mov       rcx,rsi
       7FFD4C2CA2E8 call      System.ArgumentNullException..ctor(System.String)
       7FFD4C2CA2ED mov       rcx,rsi
       7FFD4C2CA2F0 call      CORINFO_HELP_THROW
M02_L01:
       7FFD4C2CA2F5 mov       rcx,offset MT_System.ArgumentNullException
       7FFD4C2CA2FF call      CORINFO_HELP_NEWSFAST
       7FFD4C2CA304 mov       rsi,rax
       7FFD4C2CA307 mov       ecx,733
       7FFD4C2CA30C mov       rdx,7FFD4C3791D8
       7FFD4C2CA316 call      CORINFO_HELP_STRCNS
       7FFD4C2CA31B mov       rdx,rax
       7FFD4C2CA31E mov       rcx,rsi
       7FFD4C2CA321 call      System.ArgumentNullException..ctor(System.String)
       7FFD4C2CA326 mov       rcx,rsi
       7FFD4C2CA329 call      CORINFO_HELP_THROW
       7FFD4C2CA32E int       3
; Total bytes of code 335
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
       7FFD4C2B8A60 push      rdi
       7FFD4C2B8A61 push      rsi
       7FFD4C2B8A62 push      rbp
       7FFD4C2B8A63 push      rbx
       7FFD4C2B8A64 sub       rsp,28
;         sum = 0;
;         ^^^^^^^^
       7FFD4C2B8A68 mov       dword ptr [7FFD4C24ECA0],0
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
       7FFD4C2B8A72 mov       rcx,[rcx+8]
       7FFD4C2B8A76 test      rcx,rcx
       7FFD4C2B8A79 je        short M00_L02
       7FFD4C2B8A7B mov       rax,[rcx+8]
       7FFD4C2B8A7F mov       esi,[rcx+10]
       7FFD4C2B8A82 test      rax,rax
       7FFD4C2B8A85 jne       short M00_L00
       7FFD4C2B8A87 test      esi,esi
       7FFD4C2B8A89 jne       short M00_L06
       7FFD4C2B8A8B xor       edi,edi
       7FFD4C2B8A8D xor       esi,esi
       7FFD4C2B8A8F jmp       short M00_L01
M00_L00:
       7FFD4C2B8A91 mov       ecx,[rax+8]
       7FFD4C2B8A94 mov       edx,esi
       7FFD4C2B8A96 cmp       rcx,rdx
       7FFD4C2B8A99 jb        short M00_L06
       7FFD4C2B8A9B add       rax,10
       7FFD4C2B8A9F mov       rdi,rax
M00_L01:
       7FFD4C2B8AA2 jmp       short M00_L03
M00_L02:
       7FFD4C2B8AA4 xor       edi,edi
       7FFD4C2B8AA6 xor       esi,esi
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
M00_L03:
       7FFD4C2B8AA8 xor       ebx,ebx
       7FFD4C2B8AAA test      esi,esi
       7FFD4C2B8AAC jle       short M00_L05
;             sum += DoSomething(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L04:
       7FFD4C2B8AAE mov       ebp,[7FFD4C24ECA0]
       7FFD4C2B8AB4 movsxd    rcx,ebx
       7FFD4C2B8AB7 mov       ecx,[rdi+rcx*4]
       7FFD4C2B8ABA call      Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD4C2B8ABF add       eax,ebp
       7FFD4C2B8AC1 mov       [7FFD4C24ECA0],eax
       7FFD4C2B8AC7 inc       ebx
       7FFD4C2B8AC9 cmp       ebx,esi
       7FFD4C2B8ACB jl        short M00_L04
;         return sum;
;         ^^^^^^^^^^^
M00_L05:
       7FFD4C2B8ACD mov       eax,[7FFD4C24ECA0]
       7FFD4C2B8AD3 add       rsp,28
       7FFD4C2B8AD7 pop       rbx
       7FFD4C2B8AD8 pop       rbp
       7FFD4C2B8AD9 pop       rsi
       7FFD4C2B8ADA pop       rdi
       7FFD4C2B8ADB ret
M00_L06:
       7FFD4C2B8ADC call      System.ThrowHelper.ThrowArgumentOutOfRangeException()
       7FFD4C2B8AE1 int       3
; Total bytes of code 130
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD4C2D2850 lea       eax,[rcx+rcx]
       7FFD4C2D2853 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowArgumentOutOfRangeException()

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
;         sum = 0;
;         ^^^^^^^^
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
;             sum += DoSomething(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD6ED3E120 push      rdi
       7FFD6ED3E121 push      rsi
       7FFD6ED3E122 push      rbp
       7FFD6ED3E123 push      rbx
       7FFD6ED3E124 sub       rsp,28
       7FFD6ED3E128 mov       rbx,rcx
       7FFD6ED3E12B mov       rsi,7FFD6EFC52F0
       7FFD6ED3E135 xor       ecx,ecx
       7FFD6ED3E137 mov       [rsi],ecx
       7FFD6ED3E139 xor       edi,edi
       7FFD6ED3E13B mov       rcx,[rbx+8]
       7FFD6ED3E13F cmp       dword ptr [rcx+10],0
       7FFD6ED3E143 jle       short M00_L01
M00_L00:
       7FFD6ED3E145 mov       ebp,[rsi]
       7FFD6ED3E147 mov       rcx,[rbx+8]
       7FFD6ED3E14B cmp       edi,[rcx+10]
       7FFD6ED3E14E jae       short M00_L02
       7FFD6ED3E150 mov       rcx,[rcx+8]
       7FFD6ED3E154 cmp       edi,[rcx+8]
       7FFD6ED3E157 jae       short M00_L03
       7FFD6ED3E159 mov       eax,edi
       7FFD6ED3E15B mov       ecx,[rcx+rax*4+10]
       7FFD6ED3E15F call      qword ptr [7FFD6EFAEE50]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD6ED3E165 add       eax,ebp
       7FFD6ED3E167 mov       [rsi],eax
       7FFD6ED3E169 inc       edi
       7FFD6ED3E16B mov       rax,[rbx+8]
       7FFD6ED3E16F cmp       edi,[rax+10]
       7FFD6ED3E172 jl        short M00_L00
M00_L01:
       7FFD6ED3E174 mov       eax,[rsi]
       7FFD6ED3E176 add       rsp,28
       7FFD6ED3E17A pop       rbx
       7FFD6ED3E17B pop       rbp
       7FFD6ED3E17C pop       rsi
       7FFD6ED3E17D pop       rdi
       7FFD6ED3E17E ret
M00_L02:
       7FFD6ED3E17F call      qword ptr [7FFD6EFA5878]
       7FFD6ED3E185 int       3
M00_L03:
       7FFD6ED3E186 call      CORINFO_HELP_RNGCHKFAIL
       7FFD6ED3E18B int       3
; Total bytes of code 108
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD6ED3DE80 lea       eax,[rcx+rcx]
       7FFD6ED3DE83 ret
; Total bytes of code 4
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         sum = 0;
;         ^^^^^^^^
;         List.ForEach(_doSomething);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD6ED5E080 push      rbx
       7FFD6ED5E081 sub       rsp,20
       7FFD6ED5E085 mov       rdx,rcx
       7FFD6ED5E088 mov       rbx,7FFD6EFE52F0
       7FFD6ED5E092 xor       ecx,ecx
       7FFD6ED5E094 mov       [rbx],ecx
       7FFD6ED5E096 mov       rcx,[rdx+8]
       7FFD6ED5E09A mov       rdx,[rdx+10]
       7FFD6ED5E09E cmp       [rcx],ecx
       7FFD6ED5E0A0 call      qword ptr [7FFD6EE6F000]; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD6ED5E0A6 mov       eax,[rbx]
       7FFD6ED5E0A8 add       rsp,20
       7FFD6ED5E0AC pop       rbx
       7FFD6ED5E0AD ret
; Total bytes of code 46
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD6ED5E0E0 push      r15
       7FFD6ED5E0E2 push      r14
       7FFD6ED5E0E4 push      r13
       7FFD6ED5E0E6 push      rdi
       7FFD6ED5E0E7 push      rsi
       7FFD6ED5E0E8 push      rbp
       7FFD6ED5E0E9 push      rbx
       7FFD6ED5E0EA sub       rsp,20
       7FFD6ED5E0EE mov       rbx,rcx
       7FFD6ED5E0F1 mov       rsi,rdx
       7FFD6ED5E0F4 test      rsi,rsi
       7FFD6ED5E0F7 je        near ptr M01_L04
       7FFD6ED5E0FD mov       edi,[rbx+14]
       7FFD6ED5E100 xor       ebp,ebp
       7FFD6ED5E102 cmp       dword ptr [rbx+10],0
       7FFD6ED5E106 jle       near ptr M01_L03
       7FFD6ED5E10C mov       r14,[rsi+18]
       7FFD6ED5E110 mov       rcx,7FFD6F0214A0
       7FFD6ED5E11A cmp       r14,rcx
       7FFD6ED5E11D jne       short M01_L01
M01_L00:
       7FFD6ED5E11F cmp       edi,[rbx+14]
       7FFD6ED5E122 jne       near ptr M01_L03
       7FFD6ED5E128 mov       r14,[rbx+8]
       7FFD6ED5E12C cmp       ebp,[r14+8]
       7FFD6ED5E130 jae       near ptr M01_L07
       7FFD6ED5E136 mov       ecx,ebp
       7FFD6ED5E138 mov       edx,[r14+rcx*4+10]
       7FFD6ED5E13D mov       rsi,7FFD6EFE52F0
       7FFD6ED5E147 mov       r14d,[rsi]
       7FFD6ED5E14A mov       ecx,edx
       7FFD6ED5E14C call      qword ptr [7FFD6EFCEE50]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD6ED5E152 add       eax,r14d
       7FFD6ED5E155 mov       [rsi],eax
       7FFD6ED5E157 inc       ebp
       7FFD6ED5E159 cmp       ebp,[rbx+10]
       7FFD6ED5E15C jl        short M01_L00
       7FFD6ED5E15E jmp       short M01_L03
M01_L01:
       7FFD6ED5E160 cmp       edi,[rbx+14]
       7FFD6ED5E163 jne       short M01_L03
       7FFD6ED5E165 mov       rcx,[rbx+8]
       7FFD6ED5E169 cmp       ebp,[rcx+8]
       7FFD6ED5E16C jae       short M01_L07
       7FFD6ED5E16E mov       eax,ebp
       7FFD6ED5E170 mov       edx,[rcx+rax*4+10]
       7FFD6ED5E174 mov       rcx,7FFD6F0214A0
       7FFD6ED5E17E cmp       r14,rcx
       7FFD6ED5E181 jne       short M01_L05
       7FFD6ED5E183 mov       rcx,7FFD6EFE52F0
       7FFD6ED5E18D mov       r15,rcx
       7FFD6ED5E190 mov       r13d,[r15]
       7FFD6ED5E193 mov       ecx,edx
       7FFD6ED5E195 call      qword ptr [7FFD6EFCEE50]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD6ED5E19B add       eax,r13d
       7FFD6ED5E19E mov       [r15],eax
M01_L02:
       7FFD6ED5E1A1 inc       ebp
       7FFD6ED5E1A3 cmp       ebp,[rbx+10]
       7FFD6ED5E1A6 jl        short M01_L01
M01_L03:
       7FFD6ED5E1A8 cmp       edi,[rbx+14]
       7FFD6ED5E1AB jne       short M01_L06
       7FFD6ED5E1AD add       rsp,20
       7FFD6ED5E1B1 pop       rbx
       7FFD6ED5E1B2 pop       rbp
       7FFD6ED5E1B3 pop       rsi
       7FFD6ED5E1B4 pop       rdi
       7FFD6ED5E1B5 pop       r13
       7FFD6ED5E1B7 pop       r14
       7FFD6ED5E1B9 pop       r15
       7FFD6ED5E1BB ret
M01_L04:
       7FFD6ED5E1BC mov       ecx,1C
       7FFD6ED5E1C1 call      qword ptr [7FFD6EFC5B18]
       7FFD6ED5E1C7 int       3
M01_L05:
       7FFD6ED5E1C8 mov       rcx,[rsi+8]
       7FFD6ED5E1CC call      qword ptr [rsi+18]
       7FFD6ED5E1CF jmp       short M01_L02
M01_L06:
       7FFD6ED5E1D1 call      qword ptr [7FFD6EFC5E00]
       7FFD6ED5E1D7 int       3
M01_L07:
       7FFD6ED5E1D8 call      CORINFO_HELP_RNGCHKFAIL
       7FFD6ED5E1DD int       3
; Total bytes of code 254
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         sum = 0;
;         ^^^^^^^^
;         Parallel.ForEach(List, _doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD6ED6D460 push      rbp
       7FFD6ED6D461 push      r14
       7FFD6ED6D463 push      rdi
       7FFD6ED6D464 push      rsi
       7FFD6ED6D465 push      rbx
       7FFD6ED6D466 sub       rsp,80
       7FFD6ED6D46D lea       rbp,[rsp+0A0]
       7FFD6ED6D475 xor       eax,eax
       7FFD6ED6D477 mov       [rbp-40],rax
       7FFD6ED6D47B mov       rbx,7FFD6EFE52F0
       7FFD6ED6D485 xor       edx,edx
       7FFD6ED6D487 mov       [rbx],edx
       7FFD6ED6D489 mov       rsi,[rcx+8]
       7FFD6ED6D48D mov       rdi,[rcx+18]
       7FFD6ED6D491 test      rsi,rsi
       7FFD6ED6D494 je        near ptr M00_L03
       7FFD6ED6D49A test      rdi,rdi
       7FFD6ED6D49D je        near ptr M00_L04
       7FFD6ED6D4A3 mov       rdx,22861006EC8
       7FFD6ED6D4AD mov       r14,[rdx]
       7FFD6ED6D4B0 mov       rdx,[r14+18]
       7FFD6ED6D4B4 mov       [rbp-40],rdx
       7FFD6ED6D4B8 cmp       qword ptr [rbp-40],0
       7FFD6ED6D4BD jne       short M00_L02
M00_L00:
       7FFD6ED6D4BF mov       rdx,rsi
       7FFD6ED6D4C2 mov       rcx,offset MT_System.Int32[]
       7FFD6ED6D4CC call      qword ptr [7FFD6ED24330]; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFD6ED6D4D2 test      rax,rax
       7FFD6ED6D4D5 jne       near ptr M00_L05
       7FFD6ED6D4DB mov       r8,rsi
       7FFD6ED6D4DE mov       [rsp+20],rdi
       7FFD6ED6D4E3 xor       ecx,ecx
       7FFD6ED6D4E5 mov       [rsp+28],rcx
       7FFD6ED6D4EA mov       [rsp+30],rcx
       7FFD6ED6D4EF mov       [rsp+38],rcx
       7FFD6ED6D4F4 mov       [rsp+40],rcx
       7FFD6ED6D4F9 mov       [rsp+48],rcx
       7FFD6ED6D4FE mov       [rsp+50],rcx
       7FFD6ED6D503 lea       rcx,[rbp-38]
       7FFD6ED6D507 mov       r9,r14
       7FFD6ED6D50A mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD6ED6D514 call      qword ptr [7FFD6F17C918]; System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M00_L01:
       7FFD6ED6D51A mov       eax,[rbx]
       7FFD6ED6D51C add       rsp,80
       7FFD6ED6D523 pop       rbx
       7FFD6ED6D524 pop       rsi
       7FFD6ED6D525 pop       rdi
       7FFD6ED6D526 pop       r14
       7FFD6ED6D528 pop       rbp
       7FFD6ED6D529 ret
M00_L02:
       7FFD6ED6D52A mov       rdx,[rbp-40]
       7FFD6ED6D52E cmp       dword ptr [rdx+20],0
       7FFD6ED6D532 je        short M00_L00
       7FFD6ED6D534 lea       rcx,[rbp-40]
       7FFD6ED6D538 call      qword ptr [7FFD6EF8D740]
       7FFD6ED6D53E int       3
M00_L03:
       7FFD6ED6D53F mov       ecx,3C3
       7FFD6ED6D544 mov       rdx,7FFD6F194048
       7FFD6ED6D54E call      CORINFO_HELP_STRCNS
       7FFD6ED6D553 mov       rcx,rax
       7FFD6ED6D556 call      qword ptr [7FFD6EE46790]
       7FFD6ED6D55C int       3
M00_L04:
       7FFD6ED6D55D mov       ecx,38B
       7FFD6ED6D562 mov       rdx,7FFD6F194048
       7FFD6ED6D56C call      CORINFO_HELP_STRCNS
       7FFD6ED6D571 mov       rcx,rax
       7FFD6ED6D574 call      qword ptr [7FFD6EE46790]
       7FFD6ED6D57A int       3
M00_L05:
       7FFD6ED6D57B mov       [rsp+20],rdi
       7FFD6ED6D580 xor       ecx,ecx
       7FFD6ED6D582 mov       [rsp+28],rcx
       7FFD6ED6D587 mov       [rsp+30],rcx
       7FFD6ED6D58C mov       [rsp+38],rcx
       7FFD6ED6D591 mov       [rsp+40],rcx
       7FFD6ED6D596 mov       [rsp+48],rcx
       7FFD6ED6D59B mov       [rsp+50],rcx
       7FFD6ED6D5A0 lea       rcx,[rbp-38]
       7FFD6ED6D5A4 mov       r8,rax
       7FFD6ED6D5A7 mov       r9,r14
       7FFD6ED6D5AA mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD6ED6D5B4 call      qword ptr [7FFD6F17C960]
       7FFD6ED6D5BA jmp       near ptr M00_L01
; Total bytes of code 351
```
```assembly
; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFD6ED65580 push      rsi
       7FFD6ED65581 push      rbx
       7FFD6ED65582 test      rdx,rdx
       7FFD6ED65585 je        short M01_L00
       7FFD6ED65587 mov       rax,[rdx]
       7FFD6ED6558A cmp       rax,rcx
       7FFD6ED6558D jne       short M01_L01
M01_L00:
       7FFD6ED6558F mov       rax,rdx
       7FFD6ED65592 pop       rbx
       7FFD6ED65593 pop       rsi
       7FFD6ED65594 ret
M01_L01:
       7FFD6ED65595 mov       r8,22861000B50
       7FFD6ED6559F mov       r8,[r8]
       7FFD6ED655A2 add       r8,10
       7FFD6ED655A6 rorx      r10,rax,20
       7FFD6ED655AC xor       r10,rcx
       7FFD6ED655AF mov       r9,9E3779B97F4A7C15
       7FFD6ED655B9 imul      r10,r9
       7FFD6ED655BD mov       r9d,[r8]
       7FFD6ED655C0 shrx      r10,r10,r9
       7FFD6ED655C5 xor       r9d,r9d
M01_L02:
       7FFD6ED655C8 lea       r11d,[r10+1]
       7FFD6ED655CC movsxd    r11,r11d
       7FFD6ED655CF lea       r11,[r11+r11*2]
       7FFD6ED655D3 lea       r11,[r8+r11*8]
       7FFD6ED655D7 mov       ebx,[r11]
       7FFD6ED655DA mov       rsi,[r11+8]
       7FFD6ED655DE and       ebx,0FFFFFFFE
       7FFD6ED655E1 cmp       rsi,rax
       7FFD6ED655E4 jne       short M01_L03
       7FFD6ED655E6 mov       rsi,rcx
       7FFD6ED655E9 xor       rsi,[r11+10]
       7FFD6ED655ED cmp       rsi,1
       7FFD6ED655F1 jbe       short M01_L04
M01_L03:
       7FFD6ED655F3 test      ebx,ebx
       7FFD6ED655F5 je        short M01_L06
       7FFD6ED655F7 inc       r9d
       7FFD6ED655FA add       r10d,r9d
       7FFD6ED655FD and       r10d,[r8+4]
       7FFD6ED65601 cmp       r9d,8
       7FFD6ED65605 jl        short M01_L02
       7FFD6ED65607 jmp       short M01_L06
M01_L04:
       7FFD6ED65609 cmp       ebx,[r11]
       7FFD6ED6560C jne       short M01_L06
M01_L05:
       7FFD6ED6560E cmp       esi,1
       7FFD6ED65611 je        near ptr M01_L00
       7FFD6ED65617 test      esi,esi
       7FFD6ED65619 jne       short M01_L07
       7FFD6ED6561B xor       edx,edx
       7FFD6ED6561D jmp       near ptr M01_L00
M01_L06:
       7FFD6ED65622 mov       esi,2
       7FFD6ED65627 jmp       short M01_L05
M01_L07:
       7FFD6ED65629 pop       rbx
       7FFD6ED6562A pop       rsi
       7FFD6ED6562B jmp       near ptr System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny_NoCacheLookup(Void*, System.Object)
; Total bytes of code 176
```
```assembly
; System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFD6ED6DA50 push      rbp
       7FFD6ED6DA51 push      r15
       7FFD6ED6DA53 push      r14
       7FFD6ED6DA55 push      r13
       7FFD6ED6DA57 push      r12
       7FFD6ED6DA59 push      rdi
       7FFD6ED6DA5A push      rsi
       7FFD6ED6DA5B push      rbx
       7FFD6ED6DA5C sub       rsp,38
       7FFD6ED6DA60 lea       rbp,[rsp+70]
       7FFD6ED6DA65 mov       [rbp-40],rdx
       7FFD6ED6DA69 mov       rsi,rcx
       7FFD6ED6DA6C mov       rbx,rdx
       7FFD6ED6DA6F mov       r14,r8
       7FFD6ED6DA72 mov       rdi,r9
       7FFD6ED6DA75 mov       rcx,[rbx+10]
       7FFD6ED6DA79 mov       rcx,[rcx+18]
       7FFD6ED6DA7D test      rcx,rcx
       7FFD6ED6DA80 je        short M02_L00
       7FFD6ED6DA82 jmp       short M02_L01
M02_L00:
       7FFD6ED6DA84 mov       rcx,rbx
       7FFD6ED6DA87 mov       rdx,7FFD6F186698
       7FFD6ED6DA91 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFD6ED6DA96 mov       rcx,rax
M02_L01:
       7FFD6ED6DA99 call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DA9E mov       r15,rax
       7FFD6ED6DAA1 lea       rcx,[r15+8]
       7FFD6ED6DAA5 mov       rdx,[rbp+30]
       7FFD6ED6DAA9 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DAAE lea       rcx,[r15+10]
       7FFD6ED6DAB2 mov       rdx,r14
       7FFD6ED6DAB5 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DABA lea       rcx,[r15+18]
       7FFD6ED6DABE mov       rdx,[rbp+38]
       7FFD6ED6DAC2 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DAC7 lea       rcx,[r15+20]
       7FFD6ED6DACB mov       rdx,[rbp+40]
       7FFD6ED6DACF call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DAD4 lea       rcx,[r15+28]
       7FFD6ED6DAD8 mov       rdx,[rbp+48]
       7FFD6ED6DADC call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DAE1 lea       rcx,[r15+30]
       7FFD6ED6DAE5 mov       rdx,[rbp+50]
       7FFD6ED6DAE9 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DAEE cmp       qword ptr [r15+8],0
       7FFD6ED6DAF3 je        near ptr M02_L03
       7FFD6ED6DAF9 mov       rcx,[r15+10]
       7FFD6ED6DAFD mov       rax,offset MT_System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]]
       7FFD6ED6DB07 cmp       [rcx],rax
       7FFD6ED6DB0A jne       near ptr M02_L15
       7FFD6ED6DB10 mov       ebx,[rcx+10]
M02_L02:
       7FFD6ED6DB13 mov       rcx,offset MT_System.Action`1[[System.Int32, System.Private.CoreLib]]
       7FFD6ED6DB1D call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DB22 mov       r14,rax
       7FFD6ED6DB25 lea       rcx,[r14+8]
       7FFD6ED6DB29 mov       rdx,r15
       7FFD6ED6DB2C call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED6DB31 mov       rcx,7FFD6F178A68
       7FFD6ED6DB3B mov       [r14+18],rcx
       7FFD6ED6DB3F mov       [rbp+30],rdi
       7FFD6ED6DB43 mov       [rbp+38],r14
       7FFD6ED6DB47 xor       ecx,ecx
       7FFD6ED6DB49 mov       [rbp+40],rcx
       7FFD6ED6DB4D mov       [rbp+48],rcx
       7FFD6ED6DB51 mov       [rbp+50],rcx
       7FFD6ED6DB55 mov       [rbp+58],rcx
       7FFD6ED6DB59 mov       rcx,rsi
       7FFD6ED6DB5C mov       r9d,ebx
       7FFD6ED6DB5F mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD6ED6DB69 xor       r8d,r8d
       7FFD6ED6DB6C add       rsp,38
       7FFD6ED6DB70 pop       rbx
       7FFD6ED6DB71 pop       rsi
       7FFD6ED6DB72 pop       rdi
       7FFD6ED6DB73 pop       r12
       7FFD6ED6DB75 pop       r13
       7FFD6ED6DB77 pop       r14
       7FFD6ED6DB79 pop       r15
       7FFD6ED6DB7B pop       rbp
       7FFD6ED6DB7C jmp       qword ptr [7FFD6F17CBD0]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L03:
       7FFD6ED6DB82 cmp       qword ptr [r15+18],0
       7FFD6ED6DB87 je        near ptr M02_L04
       7FFD6ED6DB8D mov       rcx,offset MT_System.Action`2[[System.Int32, System.Private.CoreLib],[System.Threading.Tasks.ParallelLoopState, System.Threading.Tasks.Parallel]]
       7FFD6ED6DB97 call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DB9C mov       rbx,rax
       7FFD6ED6DB9F mov       rcx,[r15+10]
       7FFD6ED6DBA3 mov       r11,7FFD6EBE05A8
       7FFD6ED6DBAD call      qword ptr [r11]
       7FFD6ED6DBB0 mov       r14d,eax
       7FFD6ED6DBB3 mov       rcx,rbx
       7FFD6ED6DBB6 mov       rdx,r15
       7FFD6ED6DBB9 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__1(Int32, System.Threading.Tasks.ParallelLoopState)
       7FFD6ED6DBC3 call      qword ptr [7FFD6ED24210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFD6ED6DBC9 mov       [rbp+30],rdi
       7FFD6ED6DBCD xor       ecx,ecx
       7FFD6ED6DBCF mov       [rbp+38],rcx
       7FFD6ED6DBD3 mov       [rbp+40],rbx
       7FFD6ED6DBD7 mov       [rbp+48],rcx
       7FFD6ED6DBDB mov       [rbp+50],rcx
       7FFD6ED6DBDF mov       [rbp+58],rcx
       7FFD6ED6DBE3 mov       rcx,rsi
       7FFD6ED6DBE6 mov       r9d,r14d
       7FFD6ED6DBE9 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD6ED6DBF3 xor       r8d,r8d
       7FFD6ED6DBF6 add       rsp,38
       7FFD6ED6DBFA pop       rbx
       7FFD6ED6DBFB pop       rsi
       7FFD6ED6DBFC pop       rdi
       7FFD6ED6DBFD pop       r12
       7FFD6ED6DBFF pop       r13
       7FFD6ED6DC01 pop       r14
       7FFD6ED6DC03 pop       r15
       7FFD6ED6DC05 pop       rbp
       7FFD6ED6DC06 jmp       qword ptr [7FFD6F17CBD0]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L04:
       7FFD6ED6DC0C cmp       qword ptr [r15+20],0
       7FFD6ED6DC11 je        near ptr M02_L05
       7FFD6ED6DC17 mov       rcx,offset MT_System.Action`2[[System.Int32, System.Private.CoreLib],[System.Threading.Tasks.ParallelLoopState, System.Threading.Tasks.Parallel]]
       7FFD6ED6DC21 call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DC26 mov       rbx,rax
       7FFD6ED6DC29 mov       rcx,[r15+10]
       7FFD6ED6DC2D mov       r11,7FFD6EBE05A0
       7FFD6ED6DC37 call      qword ptr [r11]
       7FFD6ED6DC3A mov       r14d,eax
       7FFD6ED6DC3D mov       rcx,rbx
       7FFD6ED6DC40 mov       rdx,r15
       7FFD6ED6DC43 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__2(Int32, System.Threading.Tasks.ParallelLoopState)
       7FFD6ED6DC4D call      qword ptr [7FFD6ED24210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFD6ED6DC53 mov       [rbp+30],rdi
       7FFD6ED6DC57 xor       ecx,ecx
       7FFD6ED6DC59 mov       [rbp+38],rcx
       7FFD6ED6DC5D mov       [rbp+40],rbx
       7FFD6ED6DC61 mov       [rbp+48],rcx
       7FFD6ED6DC65 mov       [rbp+50],rcx
       7FFD6ED6DC69 mov       [rbp+58],rcx
       7FFD6ED6DC6D mov       rcx,rsi
       7FFD6ED6DC70 mov       r9d,r14d
       7FFD6ED6DC73 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFD6ED6DC7D xor       r8d,r8d
       7FFD6ED6DC80 add       rsp,38
       7FFD6ED6DC84 pop       rbx
       7FFD6ED6DC85 pop       rsi
       7FFD6ED6DC86 pop       rdi
       7FFD6ED6DC87 pop       r12
       7FFD6ED6DC89 pop       r13
       7FFD6ED6DC8B pop       r14
       7FFD6ED6DC8D pop       r15
       7FFD6ED6DC8F pop       rbp
       7FFD6ED6DC90 jmp       qword ptr [7FFD6F17CBD0]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L05:
       7FFD6ED6DC96 cmp       qword ptr [r15+28],0
       7FFD6ED6DC9B je        near ptr M02_L10
       7FFD6ED6DCA1 mov       rcx,[rbx+10]
       7FFD6ED6DCA5 mov       rcx,[rcx+20]
       7FFD6ED6DCA9 test      rcx,rcx
       7FFD6ED6DCAC je        short M02_L06
       7FFD6ED6DCAE jmp       short M02_L07
M02_L06:
       7FFD6ED6DCB0 mov       rcx,rbx
       7FFD6ED6DCB3 mov       rdx,7FFD6F186928
       7FFD6ED6DCBD call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFD6ED6DCC2 mov       rcx,rax
M02_L07:
       7FFD6ED6DCC5 call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DCCA mov       r14,rax
       7FFD6ED6DCCD mov       rcx,[r15+10]
       7FFD6ED6DCD1 mov       r11,7FFD6EBE0598
       7FFD6ED6DCDB call      qword ptr [r11]
       7FFD6ED6DCDE mov       r13d,eax
       7FFD6ED6DCE1 mov       rcx,r14
       7FFD6ED6DCE4 mov       rdx,r15
       7FFD6ED6DCE7 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__3(Int32, System.Threading.Tasks.ParallelLoopState, System.__Canon)
       7FFD6ED6DCF1 call      qword ptr [7FFD6ED24210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFD6ED6DCF7 mov       rcx,[rbx+10]
       7FFD6ED6DCFB mov       rdx,[rcx+28]
       7FFD6ED6DCFF test      rdx,rdx
       7FFD6ED6DD02 je        short M02_L08
       7FFD6ED6DD04 jmp       short M02_L09
M02_L08:
       7FFD6ED6DD06 mov       rcx,rbx
       7FFD6ED6DD09 mov       rdx,7FFD6F187878
       7FFD6ED6DD13 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFD6ED6DD18 mov       rdx,rax
M02_L09:
       7FFD6ED6DD1B mov       [rbp+30],rdi
       7FFD6ED6DD1F xor       ecx,ecx
       7FFD6ED6DD21 mov       [rbp+38],rcx
       7FFD6ED6DD25 mov       [rbp+40],rcx
       7FFD6ED6DD29 mov       [rbp+48],r14
       7FFD6ED6DD2D mov       r14,[rbp+58]
       7FFD6ED6DD31 mov       [rbp+50],r14
       7FFD6ED6DD35 mov       r12,[rbp+60]
       7FFD6ED6DD39 mov       [rbp+58],r12
       7FFD6ED6DD3D mov       rcx,rsi
       7FFD6ED6DD40 mov       r9d,r13d
       7FFD6ED6DD43 xor       r8d,r8d
       7FFD6ED6DD46 add       rsp,38
       7FFD6ED6DD4A pop       rbx
       7FFD6ED6DD4B pop       rsi
       7FFD6ED6DD4C pop       rdi
       7FFD6ED6DD4D pop       r12
       7FFD6ED6DD4F pop       r13
       7FFD6ED6DD51 pop       r14
       7FFD6ED6DD53 pop       r15
       7FFD6ED6DD55 pop       rbp
       7FFD6ED6DD56 jmp       qword ptr [7FFD6F17CBD0]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L10:
       7FFD6ED6DD5C mov       rcx,[rbx+10]
       7FFD6ED6DD60 mov       rcx,[rcx+20]
       7FFD6ED6DD64 test      rcx,rcx
       7FFD6ED6DD67 je        short M02_L11
       7FFD6ED6DD69 jmp       short M02_L12
M02_L11:
       7FFD6ED6DD6B mov       rcx,rbx
       7FFD6ED6DD6E mov       rdx,7FFD6F186928
       7FFD6ED6DD78 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFD6ED6DD7D mov       rcx,rax
M02_L12:
       7FFD6ED6DD80 call      CORINFO_HELP_NEWSFAST
       7FFD6ED6DD85 mov       r13,rax
       7FFD6ED6DD88 mov       rcx,[r15+10]
       7FFD6ED6DD8C mov       r11,7FFD6EBE0590
       7FFD6ED6DD96 call      qword ptr [r11]
       7FFD6ED6DD99 mov       [rbp-44],eax
       7FFD6ED6DD9C mov       rcx,r13
       7FFD6ED6DD9F mov       rdx,r15
       7FFD6ED6DDA2 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__4(Int32, System.Threading.Tasks.ParallelLoopState, System.__Canon)
       7FFD6ED6DDAC call      qword ptr [7FFD6ED24210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFD6ED6DDB2 mov       rcx,[rbx+10]
       7FFD6ED6DDB6 mov       rdx,[rcx+28]
       7FFD6ED6DDBA test      rdx,rdx
       7FFD6ED6DDBD je        short M02_L13
       7FFD6ED6DDBF jmp       short M02_L14
M02_L13:
       7FFD6ED6DDC1 mov       rcx,rbx
       7FFD6ED6DDC4 mov       rdx,7FFD6F187878
       7FFD6ED6DDCE call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFD6ED6DDD3 mov       rdx,rax
M02_L14:
       7FFD6ED6DDD6 mov       [rbp+30],rdi
       7FFD6ED6DDDA xor       ecx,ecx
       7FFD6ED6DDDC mov       [rbp+38],rcx
       7FFD6ED6DDE0 mov       [rbp+40],rcx
       7FFD6ED6DDE4 mov       [rbp+48],r13
       7FFD6ED6DDE8 mov       r14,[rbp+58]
       7FFD6ED6DDEC mov       [rbp+50],r14
       7FFD6ED6DDF0 mov       r12,[rbp+60]
       7FFD6ED6DDF4 mov       [rbp+58],r12
       7FFD6ED6DDF8 mov       rcx,rsi
       7FFD6ED6DDFB mov       r9d,[rbp-44]
       7FFD6ED6DDFF xor       r8d,r8d
       7FFD6ED6DE02 add       rsp,38
       7FFD6ED6DE06 pop       rbx
       7FFD6ED6DE07 pop       rsi
       7FFD6ED6DE08 pop       rdi
       7FFD6ED6DE09 pop       r12
       7FFD6ED6DE0B pop       r13
       7FFD6ED6DE0D pop       r14
       7FFD6ED6DE0F pop       r15
       7FFD6ED6DE11 pop       rbp
       7FFD6ED6DE12 jmp       qword ptr [7FFD6F17CBD0]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFD6ED6DE18 add       rsp,38
       7FFD6ED6DE1C pop       rbx
       7FFD6ED6DE1D pop       rsi
       7FFD6ED6DE1E pop       rdi
       7FFD6ED6DE1F pop       r12
       7FFD6ED6DE21 pop       r13
       7FFD6ED6DE23 pop       r14
       7FFD6ED6DE25 pop       r15
       7FFD6ED6DE27 pop       rbp
       7FFD6ED6DE28 ret
M02_L15:
       7FFD6ED6DE29 mov       r11,7FFD6EBE05B0
       7FFD6ED6DE33 call      qword ptr [r11]
       7FFD6ED6DE36 mov       ebx,eax
       7FFD6ED6DE38 jmp       near ptr M02_L02
; Total bytes of code 1005
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         sum = 0;
;         ^^^^^^^^
;         List.AsParallel().ForAll(_doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD6ED71060 push      rsi
       7FFD6ED71061 push      rbx
       7FFD6ED71062 sub       rsp,28
       7FFD6ED71066 mov       rbx,rcx
       7FFD6ED71069 mov       rsi,7FFD6EFE52F0
       7FFD6ED71073 xor       ecx,ecx
       7FFD6ED71075 mov       [rsi],ecx
       7FFD6ED71077 mov       rcx,[rbx+8]
       7FFD6ED7107B call      qword ptr [7FFD6F1548E8]; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD6ED71081 mov       rcx,rax
       7FFD6ED71084 mov       rdx,[rbx+18]
       7FFD6ED71088 call      qword ptr [7FFD6F154EA0]; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFD6ED7108E mov       eax,[rsi]
       7FFD6ED71090 add       rsp,28
       7FFD6ED71094 pop       rbx
       7FFD6ED71095 pop       rsi
       7FFD6ED71096 ret
; Total bytes of code 55
```
```assembly
; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD6ED710B0 push      rdi
       7FFD6ED710B1 push      rsi
       7FFD6ED710B2 push      rbp
       7FFD6ED710B3 push      rbx
       7FFD6ED710B4 sub       rsp,58
       7FFD6ED710B8 xor       eax,eax
       7FFD6ED710BA mov       [rsp+28],rax
       7FFD6ED710BF vxorps    xmm4,xmm4,xmm4
       7FFD6ED710C3 vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFD6ED710C9 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFD6ED710CF mov       [rsp+50],rax
       7FFD6ED710D4 mov       rbx,rcx
       7FFD6ED710D7 test      rbx,rbx
       7FFD6ED710DA je        short M01_L00
       7FFD6ED710DC mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD6ED710E6 call      CORINFO_HELP_NEWSFAST
       7FFD6ED710EB mov       rbp,rax
       7FFD6ED710EE lea       rcx,[rsp+28]
       7FFD6ED710F3 call      qword ptr [7FFD6F154CF0]; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFD6ED710F9 lea       rdi,[rbp+8]
       7FFD6ED710FD lea       rsi,[rsp+28]
       7FFD6ED71102 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD6ED71107 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD6ED7110C mov       ecx,4
       7FFD6ED71111 rep movsq
       7FFD6ED71114 lea       rcx,[rbp+38]
       7FFD6ED71118 mov       rdx,rbx
       7FFD6ED7111B call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED71120 mov       rax,rbp
       7FFD6ED71123 add       rsp,58
       7FFD6ED71127 pop       rbx
       7FFD6ED71128 pop       rbp
       7FFD6ED71129 pop       rsi
       7FFD6ED7112A pop       rdi
       7FFD6ED7112B ret
M01_L00:
       7FFD6ED7112C mov       ecx,6F1
       7FFD6ED71131 mov       rdx,7FFD6F10F258
       7FFD6ED7113B call      CORINFO_HELP_STRCNS
       7FFD6ED71140 mov       rcx,rax
       7FFD6ED71143 call      qword ptr [7FFD6EE46790]
       7FFD6ED71149 int       3
; Total bytes of code 154
```
```assembly
; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFD6ED71200 push      r15
       7FFD6ED71202 push      r14
       7FFD6ED71204 push      rdi
       7FFD6ED71205 push      rsi
       7FFD6ED71206 push      rbp
       7FFD6ED71207 push      rbx
       7FFD6ED71208 sub       rsp,58
       7FFD6ED7120C vzeroupper
       7FFD6ED7120F xor       eax,eax
       7FFD6ED71211 mov       [rsp+28],rax
       7FFD6ED71216 vxorps    xmm4,xmm4,xmm4
       7FFD6ED7121A vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFD6ED71220 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFD6ED71226 mov       [rsp+50],rax
       7FFD6ED7122B mov       rsi,rcx
       7FFD6ED7122E mov       rbx,rdx
       7FFD6ED71231 test      rsi,rsi
       7FFD6ED71234 je        near ptr M02_L00
       7FFD6ED7123A test      rbx,rbx
       7FFD6ED7123D je        near ptr M02_L01
       7FFD6ED71243 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFD6ED7124D call      CORINFO_HELP_NEWSFAST
       7FFD6ED71252 mov       rbp,rax
       7FFD6ED71255 mov       rcx,rsi
       7FFD6ED71258 call      qword ptr [7FFD6F155A28]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD6ED7125E mov       r14,rax
       7FFD6ED71261 movzx     r15d,byte ptr [r14+38]
       7FFD6ED71266 vmovdqu   ymm0,ymmword ptr [r14+8]
       7FFD6ED7126C vmovdqu   ymmword ptr [rsp+28],ymm0
       7FFD6ED71272 vmovdqu   xmm0,xmmword ptr [r14+28]
       7FFD6ED71278 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFD6ED7127E mov       byte ptr [rbp+48],3
       7FFD6ED71282 lea       rdi,[rbp+8]
       7FFD6ED71286 lea       rsi,[rsp+28]
       7FFD6ED7128B call      CORINFO_HELP_ASSIGN_BYREF
       7FFD6ED71290 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD6ED71295 mov       ecx,4
       7FFD6ED7129A rep movsq
       7FFD6ED7129D mov       [rbp+38],r15b
       7FFD6ED712A1 lea       rcx,[rbp+40]
       7FFD6ED712A5 mov       rdx,r14
       7FFD6ED712A8 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED712AD lea       rcx,[rbp+50]
       7FFD6ED712B1 mov       rdx,rbx
       7FFD6ED712B4 call      CORINFO_HELP_ASSIGN_REF
       7FFD6ED712B9 mov       rcx,rbp
       7FFD6ED712BC add       rsp,58
       7FFD6ED712C0 pop       rbx
       7FFD6ED712C1 pop       rbp
       7FFD6ED712C2 pop       rsi
       7FFD6ED712C3 pop       rdi
       7FFD6ED712C4 pop       r14
       7FFD6ED712C6 pop       r15
       7FFD6ED712C8 jmp       qword ptr [7FFD6F155B30]; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
M02_L00:
       7FFD6ED712CE mov       ecx,6F1
       7FFD6ED712D3 mov       rdx,7FFD6F10F258
       7FFD6ED712DD call      CORINFO_HELP_STRCNS
       7FFD6ED712E2 mov       rcx,rax
       7FFD6ED712E5 call      qword ptr [7FFD6EE46790]
       7FFD6ED712EB int       3
M02_L01:
       7FFD6ED712EC mov       ecx,733
       7FFD6ED712F1 mov       rdx,7FFD6F10F258
       7FFD6ED712FB call      CORINFO_HELP_STRCNS
       7FFD6ED71300 mov       rcx,rax
       7FFD6ED71303 call      qword ptr [7FFD6EE46790]
       7FFD6ED71309 int       3
; Total bytes of code 266
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
;         sum = 0;
;         ^^^^^^^^
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
;             sum += DoSomething(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD6ED6E240 push      r14
       7FFD6ED6E242 push      rdi
       7FFD6ED6E243 push      rsi
       7FFD6ED6E244 push      rbp
       7FFD6ED6E245 push      rbx
       7FFD6ED6E246 sub       rsp,20
       7FFD6ED6E24A mov       rbx,7FFD6EFF52F0
       7FFD6ED6E254 xor       eax,eax
       7FFD6ED6E256 mov       [rbx],eax
       7FFD6ED6E258 mov       rcx,[rcx+8]
       7FFD6ED6E25C test      rcx,rcx
       7FFD6ED6E25F je        short M00_L05
       7FFD6ED6E261 mov       rsi,[rcx+8]
       7FFD6ED6E265 mov       edi,[rcx+10]
       7FFD6ED6E268 test      rsi,rsi
       7FFD6ED6E26B je        short M00_L03
       7FFD6ED6E26D cmp       [rsi+8],edi
       7FFD6ED6E270 jb        short M00_L04
       7FFD6ED6E272 add       rsi,10
M00_L00:
       7FFD6ED6E276 xor       ebp,ebp
       7FFD6ED6E278 test      edi,edi
       7FFD6ED6E27A jle       short M00_L02
M00_L01:
       7FFD6ED6E27C mov       r14d,[rbx]
       7FFD6ED6E27F mov       ecx,ebp
       7FFD6ED6E281 mov       ecx,[rsi+rcx*4]
       7FFD6ED6E284 call      qword ptr [7FFD6EFDEE50]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD6ED6E28A add       eax,r14d
       7FFD6ED6E28D mov       [rbx],eax
       7FFD6ED6E28F inc       ebp
       7FFD6ED6E291 cmp       ebp,edi
       7FFD6ED6E293 jl        short M00_L01
M00_L02:
       7FFD6ED6E295 mov       eax,[rbx]
       7FFD6ED6E297 add       rsp,20
       7FFD6ED6E29B pop       rbx
       7FFD6ED6E29C pop       rbp
       7FFD6ED6E29D pop       rsi
       7FFD6ED6E29E pop       rdi
       7FFD6ED6E29F pop       r14
       7FFD6ED6E2A1 ret
M00_L03:
       7FFD6ED6E2A2 test      edi,edi
       7FFD6ED6E2A4 jne       short M00_L04
       7FFD6ED6E2A6 xor       esi,esi
       7FFD6ED6E2A8 xor       edi,edi
       7FFD6ED6E2AA jmp       short M00_L00
M00_L04:
       7FFD6ED6E2AC call      qword ptr [7FFD6EFD57E8]
       7FFD6ED6E2B2 int       3
M00_L05:
       7FFD6ED6E2B3 xor       esi,esi
       7FFD6ED6E2B5 xor       edi,edi
       7FFD6ED6E2B7 jmp       short M00_L00
; Total bytes of code 121
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD6ED6DE80 lea       eax,[rcx+rcx]
       7FFD6ED6DE83 ret
; Total bytes of code 4
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
;         sum = 0;
;         ^^^^^^^^
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
;             sum += DoSomething(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD48E3EEA0 push      rdi
       7FFD48E3EEA1 push      rsi
       7FFD48E3EEA2 push      rbp
       7FFD48E3EEA3 push      rbx
       7FFD48E3EEA4 sub       rsp,28
       7FFD48E3EEA8 mov       rbx,rcx
       7FFD48E3EEAB mov       rsi,7FFD48CDB0D8
       7FFD48E3EEB5 xor       ecx,ecx
       7FFD48E3EEB7 mov       [rsi],ecx
       7FFD48E3EEB9 xor       edi,edi
       7FFD48E3EEBB mov       rcx,[rbx+8]
       7FFD48E3EEBF cmp       dword ptr [rcx+10],0
       7FFD48E3EEC3 jle       short M00_L01
M00_L00:
       7FFD48E3EEC5 mov       ebp,[rsi]
       7FFD48E3EEC7 mov       rcx,[rbx+8]
       7FFD48E3EECB cmp       edi,[rcx+10]
       7FFD48E3EECE jae       short M00_L02
       7FFD48E3EED0 mov       rcx,[rcx+8]
       7FFD48E3EED4 cmp       edi,[rcx+8]
       7FFD48E3EED7 jae       short M00_L03
       7FFD48E3EED9 mov       ecx,[rcx+rdi*4+10]
       7FFD48E3EEDD call      qword ptr [7FFD4913D1D0]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD48E3EEE3 add       eax,ebp
       7FFD48E3EEE5 mov       [rsi],eax
       7FFD48E3EEE7 inc       edi
       7FFD48E3EEE9 mov       rax,[rbx+8]
       7FFD48E3EEED cmp       edi,[rax+10]
       7FFD48E3EEF0 jl        short M00_L00
M00_L01:
       7FFD48E3EEF2 mov       eax,[rsi]
       7FFD48E3EEF4 add       rsp,28
       7FFD48E3EEF8 pop       rbx
       7FFD48E3EEF9 pop       rbp
       7FFD48E3EEFA pop       rsi
       7FFD48E3EEFB pop       rdi
       7FFD48E3EEFC ret
M00_L02:
       7FFD48E3EEFD call      qword ptr [7FFD4913D200]
       7FFD48E3EF03 int       3
M00_L03:
       7FFD48E3EF04 call      CORINFO_HELP_RNGCHKFAIL
       7FFD48E3EF09 int       3
; Total bytes of code 106
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD48E3EBF0 lea       eax,[rcx+rcx]
       7FFD48E3EBF3 ret
; Total bytes of code 4
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         sum = 0;
;         ^^^^^^^^
;         List.ForEach(_doSomething);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD48E3EE00 push      rbx
       7FFD48E3EE01 sub       rsp,20
       7FFD48E3EE05 mov       rdx,rcx
       7FFD48E3EE08 mov       rbx,7FFD48CDB0D8
       7FFD48E3EE12 xor       ecx,ecx
       7FFD48E3EE14 mov       [rbx],ecx
       7FFD48E3EE16 mov       rcx,[rdx+8]
       7FFD48E3EE1A mov       rdx,[rdx+10]
       7FFD48E3EE1E cmp       [rcx],ecx
       7FFD48E3EE20 call      qword ptr [7FFD4913D290]; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD48E3EE26 mov       eax,[rbx]
       7FFD48E3EE28 add       rsp,20
       7FFD48E3EE2C pop       rbx
       7FFD48E3EE2D ret
; Total bytes of code 46
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFD48E3EE60 push      r15
       7FFD48E3EE62 push      r14
       7FFD48E3EE64 push      r13
       7FFD48E3EE66 push      rdi
       7FFD48E3EE67 push      rsi
       7FFD48E3EE68 push      rbp
       7FFD48E3EE69 push      rbx
       7FFD48E3EE6A sub       rsp,20
       7FFD48E3EE6E mov       rbx,rcx
       7FFD48E3EE71 mov       rsi,rdx
       7FFD48E3EE74 test      rsi,rsi
       7FFD48E3EE77 je        near ptr M01_L06
       7FFD48E3EE7D mov       edi,[rbx+14]
       7FFD48E3EE80 xor       ebp,ebp
       7FFD48E3EE82 cmp       dword ptr [rbx+10],0
       7FFD48E3EE86 jle       short M01_L01
       7FFD48E3EE88 mov       r14,[rsi+18]
       7FFD48E3EE8C mov       rcx,7FFD48FF8D98
       7FFD48E3EE96 cmp       r14,rcx
       7FFD48E3EE99 jne       short M01_L02
M01_L00:
       7FFD48E3EE9B cmp       edi,[rbx+14]
       7FFD48E3EE9E jne       short M01_L01
       7FFD48E3EEA0 mov       r15,[rbx+8]
       7FFD48E3EEA4 cmp       ebp,[r15+8]
       7FFD48E3EEA8 jae       near ptr M01_L07
       7FFD48E3EEAE mov       ecx,ebp
       7FFD48E3EEB0 mov       edx,[r15+rcx*4+10]
       7FFD48E3EEB5 mov       r13,7FFD48CDB0D8
       7FFD48E3EEBF mov       esi,[r13]
       7FFD48E3EEC3 mov       ecx,edx
       7FFD48E3EEC5 call      qword ptr [7FFD4913D1D0]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD48E3EECB add       eax,esi
       7FFD48E3EECD mov       [r13],eax
       7FFD48E3EED1 inc       ebp
       7FFD48E3EED3 cmp       ebp,[rbx+10]
       7FFD48E3EED6 jl        short M01_L00
M01_L01:
       7FFD48E3EED8 cmp       edi,[rbx+14]
       7FFD48E3EEDB jne       short M01_L05
       7FFD48E3EEDD add       rsp,20
       7FFD48E3EEE1 pop       rbx
       7FFD48E3EEE2 pop       rbp
       7FFD48E3EEE3 pop       rsi
       7FFD48E3EEE4 pop       rdi
       7FFD48E3EEE5 pop       r13
       7FFD48E3EEE7 pop       r14
       7FFD48E3EEE9 pop       r15
       7FFD48E3EEEB ret
M01_L02:
       7FFD48E3EEEC cmp       edi,[rbx+14]
       7FFD48E3EEEF jne       short M01_L01
       7FFD48E3EEF1 mov       r15,[rbx+8]
       7FFD48E3EEF5 cmp       ebp,[r15+8]
       7FFD48E3EEF9 jae       short M01_L07
       7FFD48E3EEFB mov       ecx,ebp
       7FFD48E3EEFD mov       edx,[r15+rcx*4+10]
       7FFD48E3EF02 mov       rcx,7FFD48FF8D98
       7FFD48E3EF0C cmp       r14,rcx
       7FFD48E3EF0F jne       short M01_L04
       7FFD48E3EF11 mov       r13,7FFD48CDB0D8
       7FFD48E3EF1B mov       r15d,[r13]
       7FFD48E3EF1F mov       ecx,edx
       7FFD48E3EF21 call      qword ptr [7FFD4913D1D0]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD48E3EF27 add       eax,r15d
       7FFD48E3EF2A mov       [r13],eax
M01_L03:
       7FFD48E3EF2E inc       ebp
       7FFD48E3EF30 cmp       ebp,[rbx+10]
       7FFD48E3EF33 jl        short M01_L02
       7FFD48E3EF35 jmp       short M01_L01
M01_L04:
       7FFD48E3EF37 mov       rcx,[rsi+8]
       7FFD48E3EF3B call      qword ptr [rsi+18]
       7FFD48E3EF3E jmp       short M01_L03
M01_L05:
       7FFD48E3EF40 call      qword ptr [7FFD48FF7A98]
       7FFD48E3EF46 int       3
M01_L06:
       7FFD48E3EF47 mov       ecx,1C
       7FFD48E3EF4C call      qword ptr [7FFD48FF7B88]
       7FFD48E3EF52 int       3
M01_L07:
       7FFD48E3EF53 call      CORINFO_HELP_RNGCHKFAIL
       7FFD48E3EF58 int       3
; Total bytes of code 249
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         sum = 0;
;         ^^^^^^^^
;         Parallel.ForEach(List, _doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD48E1E080 push      rbp
       7FFD48E1E081 push      r14
       7FFD48E1E083 push      rdi
       7FFD48E1E084 push      rsi
       7FFD48E1E085 push      rbx
       7FFD48E1E086 sub       rsp,80
       7FFD48E1E08D lea       rbp,[rsp+0A0]
       7FFD48E1E095 xor       eax,eax
       7FFD48E1E097 mov       [rbp-40],rax
       7FFD48E1E09B mov       rbx,7FFD48CAB0D8
       7FFD48E1E0A5 xor       edx,edx
       7FFD48E1E0A7 mov       [rbx],edx
       7FFD48E1E0A9 mov       rsi,[rcx+8]
       7FFD48E1E0AD mov       rdi,[rcx+18]
       7FFD48E1E0B1 test      rsi,rsi
       7FFD48E1E0B4 je        near ptr M00_L03
       7FFD48E1E0BA test      rdi,rdi
       7FFD48E1E0BD je        near ptr M00_L04
       7FFD48E1E0C3 mov       rdx,2431DC01318
       7FFD48E1E0CD mov       r14,[rdx]
       7FFD48E1E0D0 mov       rdx,[r14+18]
       7FFD48E1E0D4 mov       [rbp-40],rdx
       7FFD48E1E0D8 cmp       qword ptr [rbp-40],0
       7FFD48E1E0DD jne       short M00_L02
M00_L00:
       7FFD48E1E0DF mov       rdx,rsi
       7FFD48E1E0E2 mov       rcx,offset MT_System.Int32[]
       7FFD48E1E0EC call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFD48E1E0F1 test      rax,rax
       7FFD48E1E0F4 jne       near ptr M00_L05
       7FFD48E1E0FA mov       [rsp+20],rdi
       7FFD48E1E0FF xor       ecx,ecx
       7FFD48E1E101 mov       [rsp+28],rcx
       7FFD48E1E106 mov       [rsp+30],rcx
       7FFD48E1E10B mov       [rsp+38],rcx
       7FFD48E1E110 mov       [rsp+40],rcx
       7FFD48E1E115 mov       [rsp+48],rcx
       7FFD48E1E11A mov       [rsp+50],rcx
       7FFD48E1E11F lea       rcx,[rbp-38]
       7FFD48E1E123 mov       r8,rsi
       7FFD48E1E126 mov       r9,r14
       7FFD48E1E129 mov       rdx,7FFD491D2310
       7FFD48E1E133 call      qword ptr [7FFD491C46F0]
M00_L01:
       7FFD48E1E139 mov       eax,[rbx]
       7FFD48E1E13B add       rsp,80
       7FFD48E1E142 pop       rbx
       7FFD48E1E143 pop       rsi
       7FFD48E1E144 pop       rdi
       7FFD48E1E145 pop       r14
       7FFD48E1E147 pop       rbp
       7FFD48E1E148 ret
M00_L02:
       7FFD48E1E149 mov       rdx,[rbp-40]
       7FFD48E1E14D cmp       dword ptr [rdx+20],0
       7FFD48E1E151 je        short M00_L00
       7FFD48E1E153 jmp       near ptr M00_L06
M00_L03:
       7FFD48E1E158 mov       ecx,3C3
       7FFD48E1E15D mov       rdx,7FFD491BE3C8
       7FFD48E1E167 call      CORINFO_HELP_STRCNS
       7FFD48E1E16C mov       rcx,rax
       7FFD48E1E16F call      qword ptr [7FFD491CF0A8]
       7FFD48E1E175 int       3
M00_L04:
       7FFD48E1E176 mov       ecx,38B
       7FFD48E1E17B mov       rdx,7FFD491BE3C8
       7FFD48E1E185 call      CORINFO_HELP_STRCNS
       7FFD48E1E18A mov       rcx,rax
       7FFD48E1E18D call      qword ptr [7FFD491CF0A8]
       7FFD48E1E193 int       3
M00_L05:
       7FFD48E1E194 mov       [rsp+20],rdi
       7FFD48E1E199 xor       ecx,ecx
       7FFD48E1E19B mov       [rsp+28],rcx
       7FFD48E1E1A0 mov       [rsp+30],rcx
       7FFD48E1E1A5 mov       [rsp+38],rcx
       7FFD48E1E1AA mov       [rsp+40],rcx
       7FFD48E1E1AF mov       [rsp+48],rcx
       7FFD48E1E1B4 mov       [rsp+50],rcx
       7FFD48E1E1B9 lea       rcx,[rbp-38]
       7FFD48E1E1BD mov       r8,rax
       7FFD48E1E1C0 mov       r9,r14
       7FFD48E1E1C3 mov       rdx,7FFD49291B58
       7FFD48E1E1CD call      qword ptr [7FFD491C4738]
       7FFD48E1E1D3 jmp       near ptr M00_L01
M00_L06:
       7FFD48E1E1D8 lea       rcx,[rbp-40]
       7FFD48E1E1DC call      qword ptr [7FFD491C4120]
       7FFD48E1E1E2 int       3
; Total bytes of code 355
```
```assembly
; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFD48E153A0 push      rsi
       7FFD48E153A1 push      rbx
       7FFD48E153A2 test      rdx,rdx
       7FFD48E153A5 je        short M01_L00
       7FFD48E153A7 mov       r8,[rdx]
       7FFD48E153AA cmp       r8,rcx
       7FFD48E153AD jne       short M01_L01
M01_L00:
       7FFD48E153AF mov       rax,rdx
       7FFD48E153B2 pop       rbx
       7FFD48E153B3 pop       rsi
       7FFD48E153B4 ret
M01_L01:
       7FFD48E153B5 mov       rax,2431DC00038
       7FFD48E153BF mov       rax,[rax]
       7FFD48E153C2 add       rax,10
       7FFD48E153C6 rorx      r10,r8,20
       7FFD48E153CC xor       r10,rcx
       7FFD48E153CF mov       r9,9E3779B97F4A7C15
       7FFD48E153D9 imul      r10,r9
       7FFD48E153DD mov       r9d,[rax]
       7FFD48E153E0 shrx      r10,r10,r9
       7FFD48E153E5 xor       r9d,r9d
M01_L02:
       7FFD48E153E8 lea       r11d,[r10+1]
       7FFD48E153EC movsxd    r11,r11d
       7FFD48E153EF lea       r11,[r11+r11*2]
       7FFD48E153F3 lea       r11,[rax+r11*8]
       7FFD48E153F7 mov       ebx,[r11]
       7FFD48E153FA mov       rsi,[r11+8]
       7FFD48E153FE and       ebx,0FFFFFFFE
       7FFD48E15401 cmp       rsi,r8
       7FFD48E15404 jne       short M01_L04
       7FFD48E15406 mov       rsi,rcx
       7FFD48E15409 xor       rsi,[r11+10]
       7FFD48E1540D cmp       rsi,1
       7FFD48E15411 ja        short M01_L04
       7FFD48E15413 cmp       ebx,[r11]
       7FFD48E15416 jne       short M01_L05
M01_L03:
       7FFD48E15418 cmp       esi,1
       7FFD48E1541B je        short M01_L00
       7FFD48E1541D test      esi,esi
       7FFD48E1541F jne       short M01_L06
       7FFD48E15421 xor       edx,edx
       7FFD48E15423 jmp       short M01_L00
M01_L04:
       7FFD48E15425 test      ebx,ebx
       7FFD48E15427 je        short M01_L05
       7FFD48E15429 inc       r9d
       7FFD48E1542C add       r10d,r9d
       7FFD48E1542F and       r10d,[rax+4]
       7FFD48E15433 cmp       r9d,8
       7FFD48E15437 jl        short M01_L02
M01_L05:
       7FFD48E15439 mov       esi,2
       7FFD48E1543E jmp       short M01_L03
M01_L06:
       7FFD48E15440 pop       rbx
       7FFD48E15441 pop       rsi
       7FFD48E15442 jmp       near ptr System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny_NoCacheLookup(Void*, System.Object)
; Total bytes of code 167
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         sum = 0;
;         ^^^^^^^^
;         List.AsParallel().ForAll(_doSomethingParallel);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD48E32630 push      r15
       7FFD48E32632 push      r14
       7FFD48E32634 push      rdi
       7FFD48E32635 push      rsi
       7FFD48E32636 push      rbp
       7FFD48E32637 push      rbx
       7FFD48E32638 sub       rsp,88
       7FFD48E3263F xor       eax,eax
       7FFD48E32641 mov       [rsp+28],rax
       7FFD48E32646 vxorps    xmm4,xmm4,xmm4
       7FFD48E3264A vmovdqu   ymmword ptr [rsp+30],ymm4
       7FFD48E32650 vmovdqu   ymmword ptr [rsp+50],ymm4
       7FFD48E32656 vmovdqa   xmmword ptr [rsp+70],xmm4
       7FFD48E3265C mov       [rsp+80],rax
       7FFD48E32664 mov       rbx,rcx
       7FFD48E32667 mov       rbp,7FFD48CBB0D8
       7FFD48E32671 xor       ecx,ecx
       7FFD48E32673 mov       [rbp],ecx
       7FFD48E32676 mov       r14,[rbx+8]
       7FFD48E3267A test      r14,r14
       7FFD48E3267D je        near ptr M00_L00
       7FFD48E32683 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E3268D call      CORINFO_HELP_NEWSFAST
       7FFD48E32692 mov       r15,rax
       7FFD48E32695 lea       rcx,[rsp+58]
       7FFD48E3269A call      qword ptr [7FFD4911D518]; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFD48E326A0 lea       rdi,[r15+8]
       7FFD48E326A4 lea       rsi,[rsp+58]
       7FFD48E326A9 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD48E326AE call      CORINFO_HELP_ASSIGN_BYREF
       7FFD48E326B3 mov       ecx,4
       7FFD48E326B8 rep movsq
       7FFD48E326BB lea       rcx,[r15+38]
       7FFD48E326BF mov       rdx,r14
       7FFD48E326C2 call      CORINFO_HELP_ASSIGN_REF
       7FFD48E326C7 mov       rbx,[rbx+18]
       7FFD48E326CB test      rbx,rbx
       7FFD48E326CE je        near ptr M00_L01
       7FFD48E326D4 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E326DE call      CORINFO_HELP_NEWSFAST
       7FFD48E326E3 mov       r14,rax
       7FFD48E326E6 mov       rcx,r15
       7FFD48E326E9 call      qword ptr [7FFD4911D8A8]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD48E326EF mov       rdx,rax
       7FFD48E326F2 movzx     r8d,byte ptr [rdx+38]
       7FFD48E326F7 vmovdqu   ymm0,ymmword ptr [rdx+8]
       7FFD48E326FC vmovdqu   ymmword ptr [rsp+28],ymm0
       7FFD48E32702 vmovdqu   xmm0,xmmword ptr [rdx+28]
       7FFD48E32707 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFD48E3270D mov       byte ptr [r14+48],3
       7FFD48E32712 lea       rdi,[r14+8]
       7FFD48E32716 lea       rsi,[rsp+28]
       7FFD48E3271B call      CORINFO_HELP_ASSIGN_BYREF
       7FFD48E32720 call      CORINFO_HELP_ASSIGN_BYREF
       7FFD48E32725 mov       ecx,4
       7FFD48E3272A rep movsq
       7FFD48E3272D mov       [r14+38],r8b
       7FFD48E32731 lea       rcx,[r14+40]
       7FFD48E32735 call      CORINFO_HELP_ASSIGN_REF
       7FFD48E3273A lea       rcx,[r14+50]
       7FFD48E3273E mov       rdx,rbx
       7FFD48E32741 call      CORINFO_HELP_ASSIGN_REF
       7FFD48E32746 mov       rcx,r14
       7FFD48E32749 call      qword ptr [7FFD4911DAA0]; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
       7FFD48E3274F mov       eax,[rbp]
       7FFD48E32752 vzeroupper
       7FFD48E32755 add       rsp,88
       7FFD48E3275C pop       rbx
       7FFD48E3275D pop       rbp
       7FFD48E3275E pop       rsi
       7FFD48E3275F pop       rdi
       7FFD48E32760 pop       r14
       7FFD48E32762 pop       r15
       7FFD48E32764 ret
M00_L00:
       7FFD48E32765 mov       ecx,6F1
       7FFD48E3276A mov       rdx,7FFD49185E90
       7FFD48E32774 call      CORINFO_HELP_STRCNS
       7FFD48E32779 mov       rcx,rax
       7FFD48E3277C call      qword ptr [7FFD491DEDC0]
       7FFD48E32782 int       3
M00_L01:
       7FFD48E32783 mov       ecx,733
       7FFD48E32788 mov       rdx,7FFD49185E90
       7FFD48E32792 call      CORINFO_HELP_STRCNS
       7FFD48E32797 mov       rcx,rax
       7FFD48E3279A call      qword ptr [7FFD491DEDC0]
       7FFD48E327A0 int       3
; Total bytes of code 369
```
```assembly
; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFD48E307C0 push      rsi
       7FFD48E307C1 push      rbx
       7FFD48E307C2 sub       rsp,28
       7FFD48E307C6 mov       rbx,rcx
       7FFD48E307C9 mov       rcx,offset MT_System.Linq.Parallel.CancellationState
       7FFD48E307D3 call      CORINFO_HELP_NEWSFAST
       7FFD48E307D8 mov       rsi,rax
       7FFD48E307DB xor       ecx,ecx
       7FFD48E307DD mov       [rsi+20],rcx
       7FFD48E307E1 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFD48E307EB call      CORINFO_HELP_NEWSFAST
       7FFD48E307F0 mov       byte ptr [rax+8],0
       7FFD48E307F4 lea       rcx,[rsi+18]
       7FFD48E307F8 mov       rdx,rax
       7FFD48E307FB call      CORINFO_HELP_ASSIGN_REF
       7FFD48E30800 xor       ecx,ecx
       7FFD48E30802 mov       [rbx],rcx
       7FFD48E30805 lea       rcx,[rbx+8]
       7FFD48E30809 mov       rdx,rsi
       7FFD48E3080C call      CORINFO_HELP_CHECKED_ASSIGN_REF
       7FFD48E30811 mov       dword ptr [rbx+10],0FFFFFFFF
       7FFD48E30818 mov       byte ptr [rbx+14],0
       7FFD48E3081C xor       eax,eax
       7FFD48E3081E mov       [rbx+18],eax
       7FFD48E30821 mov       byte ptr [rbx+1C],0
       7FFD48E30825 mov       [rbx+20],eax
       7FFD48E30828 mov       byte ptr [rbx+24],0
       7FFD48E3082C mov       [rbx+28],eax
       7FFD48E3082F mov       rax,rbx
       7FFD48E30832 add       rsp,28
       7FFD48E30836 pop       rbx
       7FFD48E30837 pop       rsi
       7FFD48E30838 ret
; Total bytes of code 121
```
```assembly
; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFD48E32A20 push      rdi
       7FFD48E32A21 push      rsi
       7FFD48E32A22 push      rbp
       7FFD48E32A23 push      rbx
       7FFD48E32A24 sub       rsp,28
       7FFD48E32A28 mov       rbx,rcx
       7FFD48E32A2B mov       rax,rbx
       7FFD48E32A2E test      rax,rax
       7FFD48E32A31 je        short M02_L00
       7FFD48E32A33 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32A3D cmp       [rax],rcx
       7FFD48E32A40 jne       near ptr M02_L04
       7FFD48E32A46 xor       eax,eax
M02_L00:
       7FFD48E32A48 test      rax,rax
       7FFD48E32A4B jne       near ptr M02_L03
       7FFD48E32A51 mov       rsi,rbx
       7FFD48E32A54 test      rsi,rsi
       7FFD48E32A57 je        short M02_L01
       7FFD48E32A59 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32A63 cmp       [rsi],rcx
       7FFD48E32A66 jne       near ptr M02_L05
       7FFD48E32A6C xor       esi,esi
M02_L01:
       7FFD48E32A6E test      rsi,rsi
       7FFD48E32A71 jne       near ptr M02_L06
       7FFD48E32A77 mov       rcx,offset MT_System.Linq.Parallel.ScanQueryOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32A81 call      CORINFO_HELP_NEWSFAST
       7FFD48E32A86 mov       rsi,rax
       7FFD48E32A89 mov       rcx,offset MT_System.Linq.Parallel.CancellationState
       7FFD48E32A93 call      CORINFO_HELP_NEWSFAST
       7FFD48E32A98 mov       rdi,rax
       7FFD48E32A9B xor       ecx,ecx
       7FFD48E32A9D mov       [rdi+20],rcx
       7FFD48E32AA1 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFD48E32AAB call      CORINFO_HELP_NEWSFAST
       7FFD48E32AB0 mov       byte ptr [rax+8],0
       7FFD48E32AB4 lea       rcx,[rdi+18]
       7FFD48E32AB8 mov       rdx,rax
       7FFD48E32ABB call      CORINFO_HELP_ASSIGN_REF
       7FFD48E32AC0 lea       rbp,[rsi+8]
       7FFD48E32AC4 xor       ecx,ecx
       7FFD48E32AC6 mov       [rbp],rcx
       7FFD48E32ACA lea       rcx,[rbp+8]
       7FFD48E32ACE mov       rdx,rdi
       7FFD48E32AD1 call      CORINFO_HELP_ASSIGN_REF
       7FFD48E32AD6 mov       dword ptr [rbp+10],0FFFFFFFF
       7FFD48E32ADD mov       byte ptr [rbp+14],0
       7FFD48E32AE1 xor       ecx,ecx
       7FFD48E32AE3 mov       [rbp+18],ecx
       7FFD48E32AE6 mov       byte ptr [rbp+1C],0
       7FFD48E32AEA mov       [rbp+20],ecx
       7FFD48E32AED mov       byte ptr [rbp+24],0
       7FFD48E32AF1 mov       [rbp+28],ecx
       7FFD48E32AF4 mov       byte ptr [rsi+38],0
       7FFD48E32AF8 test      rbx,rbx
       7FFD48E32AFB je        short M02_L02
       7FFD48E32AFD mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32B07 cmp       [rbx],rcx
       7FFD48E32B0A jne       short M02_L02
       7FFD48E32B0C mov       rbx,[rbx+38]
M02_L02:
       7FFD48E32B10 lea       rcx,[rsi+40]
       7FFD48E32B14 mov       rdx,rbx
       7FFD48E32B17 call      CORINFO_HELP_ASSIGN_REF
       7FFD48E32B1C mov       rax,rsi
M02_L03:
       7FFD48E32B1F add       rsp,28
       7FFD48E32B23 pop       rbx
       7FFD48E32B24 pop       rbp
       7FFD48E32B25 pop       rsi
       7FFD48E32B26 pop       rdi
       7FFD48E32B27 ret
M02_L04:
       7FFD48E32B28 mov       rdx,rbx
       7FFD48E32B2B mov       rcx,offset MT_System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32B35 call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfClass(Void*, System.Object)
       7FFD48E32B3A jmp       near ptr M02_L00
M02_L05:
       7FFD48E32B3F mov       rdx,rbx
       7FFD48E32B42 mov       rcx,offset MT_System.Linq.OrderedParallelQuery`1[[System.Int32, System.Private.CoreLib]]
       7FFD48E32B4C call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfClass(Void*, System.Object)
       7FFD48E32B51 mov       rsi,rax
       7FFD48E32B54 jmp       near ptr M02_L01
M02_L06:
       7FFD48E32B59 mov       rax,[rsi+38]
       7FFD48E32B5D jmp       short M02_L03
; Total bytes of code 319
```
```assembly
; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
       7FFD48E32B80 push      r15
       7FFD48E32B82 push      r14
       7FFD48E32B84 push      rdi
       7FFD48E32B85 push      rsi
       7FFD48E32B86 push      rbp
       7FFD48E32B87 push      rbx
       7FFD48E32B88 sub       rsp,0C8
       7FFD48E32B8F vxorps    xmm4,xmm4,xmm4
       7FFD48E32B93 vmovdqu   ymmword ptr [rsp+30],ymm4
       7FFD48E32B99 vmovdqu   ymmword ptr [rsp+50],ymm4
       7FFD48E32B9F vmovdqu   ymmword ptr [rsp+70],ymm4
       7FFD48E32BA5 vmovdqu   ymmword ptr [rsp+90],ymm4
       7FFD48E32BAE vmovdqa   xmmword ptr [rsp+0B0],xmm4
       7FFD48E32BB7 xor       eax,eax
       7FFD48E32BB9 mov       [rsp+0C0],rax
       7FFD48E32BC1 mov       rbx,rcx
       7FFD48E32BC4 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFD48E32BCE call      CORINFO_HELP_NEWSFAST
       7FFD48E32BD3 mov       rsi,rax
       7FFD48E32BD6 mov       byte ptr [rsi+8],0
       7FFD48E32BDA mov       rcx,offset MT_System.Threading.CancellationTokenSource
       7FFD48E32BE4 call      CORINFO_HELP_NEWSFAST
       7FFD48E32BE9 mov       r8,rax
       7FFD48E32BEC vmovdqu   ymm0,ymmword ptr [rbx+8]
       7FFD48E32BF1 vmovdqu   ymmword ptr [rsp+68],ymm0
       7FFD48E32BF7 vmovdqu   xmm0,xmmword ptr [rbx+28]
       7FFD48E32BFC vmovdqu   xmmword ptr [rsp+88],xmm0
       7FFD48E32C05 lea       rcx,[rsp+68]
       7FFD48E32C0A lea       rdx,[rsp+68]
       7FFD48E32C0F mov       r9,rsi
       7FFD48E32C12 call      qword ptr [7FFD4911DAD0]; System.Linq.Parallel.QuerySettings.WithPerExecutionSettings(System.Threading.CancellationTokenSource, System.Linq.Parallel.Shared`1<Boolean>)
       7FFD48E32C18 lea       rcx,[rsp+68]
       7FFD48E32C1D lea       rdx,[rsp+98]
       7FFD48E32C25 call      qword ptr [7FFD4911DE18]; System.Linq.Parallel.QuerySettings.WithDefaults()
       7FFD48E32C2B mov       rcx,14CA38011F8
       7FFD48E32C35 mov       rsi,[rcx]
       7FFD48E32C38 mov       rcx,rsi
       7FFD48E32C3B mov       edi,[rsp+0A8]
       7FFD48E32C42 mov       edx,edi
       7FFD48E32C44 call      qword ptr [7FFD4911DE48]; System.Linq.Parallel.PlinqEtwProvider.ParallelQueryBegin(Int32)
       7FFD48E32C4A mov       byte ptr [rsp+60],1
       7FFD48E32C4F mov       dword ptr [rsp+64],3
       7FFD48E32C57 vmovdqu   ymm0,ymmword ptr [rsp+98]
       7FFD48E32C60 vmovdqu   ymmword ptr [rsp+30],ymm0
       7FFD48E32C66 vmovdqu   xmm0,xmmword ptr [rsp+0B8]
       7FFD48E32C6F vmovdqu   xmmword ptr [rsp+50],xmm0
       7FFD48E32C75 mov       rdx,[rsp+60]
       7FFD48E32C7A lea       rcx,[rsp+30]
       7FFD48E32C7F mov       [rsp+20],rcx
       7FFD48E32C84 mov       rcx,rbx
       7FFD48E32C87 mov       r8d,1
       7FFD48E32C8D mov       r9d,1
       7FFD48E32C93 call      qword ptr [7FFD4911DE78]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].GetOpenedEnumerator(System.Nullable`1<System.Linq.ParallelMergeOptions>, Boolean, Boolean, System.Linq.Parallel.QuerySettings)
       7FFD48E32C99 mov       rcx,[rsp+0A0]
       7FFD48E32CA1 mov       rbx,[rcx+10]
       7FFD48E32CA5 mov       rcx,offset MT_System.Threading.CancellationTokenSource+Linked1CancellationTokenSource
       7FFD48E32CAF cmp       [rbx],rcx
       7FFD48E32CB2 jne       near ptr M03_L03
       7FFD48E32CB8 cmp       byte ptr [rbx+24],0
       7FFD48E32CBC jne       short M03_L01
       7FFD48E32CBE lea       rbp,[rbx+28]
       7FFD48E32CC2 mov       r14,[rbp]
       7FFD48E32CC6 test      r14,r14
       7FFD48E32CC9 jne       short M03_L02
M03_L00:
       7FFD48E32CCB mov       rcx,rbx
       7FFD48E32CCE mov       edx,1
       7FFD48E32CD3 call      qword ptr [7FFD4918E280]; System.Threading.CancellationTokenSource.Dispose(Boolean)
M03_L01:
       7FFD48E32CD9 mov       rcx,rbx
       7FFD48E32CDC call      System.GC._SuppressFinalize(System.Object)
       7FFD48E32CE1 mov       rcx,rsi
       7FFD48E32CE4 mov       edx,edi
       7FFD48E32CE6 call      qword ptr [7FFD491D44C8]; System.Linq.Parallel.PlinqEtwProvider.ParallelQueryEnd(Int32)
       7FFD48E32CEC nop
       7FFD48E32CED vzeroupper
       7FFD48E32CF0 add       rsp,0C8
       7FFD48E32CF7 pop       rbx
       7FFD48E32CF8 pop       rbp
       7FFD48E32CF9 pop       rsi
       7FFD48E32CFA pop       rdi
       7FFD48E32CFB pop       r14
       7FFD48E32CFD pop       r15
       7FFD48E32CFF ret
M03_L02:
       7FFD48E32D00 mov       rcx,[r14+8]
       7FFD48E32D04 mov       rdx,[rbp+8]
       7FFD48E32D08 mov       r8,r14
       7FFD48E32D0B cmp       [rcx],ecx
       7FFD48E32D0D call      qword ptr [7FFD491D44B0]; System.Threading.CancellationTokenSource+Registrations.Unregister(Int64, CallbackNode)
       7FFD48E32D13 test      eax,eax
       7FFD48E32D15 jne       short M03_L00
       7FFD48E32D17 mov       rbp,[rbp+8]
       7FFD48E32D1B mov       rax,[r14+8]
       7FFD48E32D1F mov       rax,[rax+8]
       7FFD48E32D23 cmp       dword ptr [rax+20],0
       7FFD48E32D27 je        short M03_L00
       7FFD48E32D29 cmp       dword ptr [rax+20],2
       7FFD48E32D2D je        short M03_L00
       7FFD48E32D2F mov       rax,[r14+8]
       7FFD48E32D33 mov       r15d,[rax+30]
       7FFD48E32D37 call      CORINFO_HELP_GETCURRENTMANAGEDTHREADID
       7FFD48E32D3C cmp       r15d,eax
       7FFD48E32D3F je        short M03_L00
       7FFD48E32D41 mov       rcx,[r14+8]
       7FFD48E32D45 mov       rdx,rbp
       7FFD48E32D48 cmp       [rcx],ecx
       7FFD48E32D4A call      qword ptr [7FFD491DF840]
       7FFD48E32D50 jmp       near ptr M03_L00
M03_L03:
       7FFD48E32D55 mov       rcx,rbx
       7FFD48E32D58 mov       edx,1
       7FFD48E32D5D mov       rax,[rbx]
       7FFD48E32D60 mov       rax,[rax+40]
       7FFD48E32D64 call      qword ptr [rax+28]
       7FFD48E32D67 jmp       near ptr M03_L01
; Total bytes of code 492
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
;         sum = 0;
;         ^^^^^^^^
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
;             sum += DoSomething(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFD48E2EF00 push      r14
       7FFD48E2EF02 push      rdi
       7FFD48E2EF03 push      rsi
       7FFD48E2EF04 push      rbp
       7FFD48E2EF05 push      rbx
       7FFD48E2EF06 sub       rsp,20
       7FFD48E2EF0A mov       rbx,7FFD48CCB0D8
       7FFD48E2EF14 xor       eax,eax
       7FFD48E2EF16 mov       [rbx],eax
       7FFD48E2EF18 mov       rcx,[rcx+8]
       7FFD48E2EF1C xor       esi,esi
       7FFD48E2EF1E test      rcx,rcx
       7FFD48E2EF21 je        short M00_L00
       7FFD48E2EF23 mov       eax,[rcx+10]
       7FFD48E2EF26 mov       rsi,[rcx+8]
       7FFD48E2EF2A cmp       [rsi+8],eax
       7FFD48E2EF2D jb        short M00_L03
       7FFD48E2EF2F add       rsi,10
M00_L00:
       7FFD48E2EF33 mov       edi,eax
       7FFD48E2EF35 test      edi,edi
       7FFD48E2EF37 jle       short M00_L02
       7FFD48E2EF39 xor       ebp,ebp
M00_L01:
       7FFD48E2EF3B mov       r14d,[rbx]
       7FFD48E2EF3E mov       ecx,[rsi+rbp]
       7FFD48E2EF41 call      qword ptr [7FFD4912D1D0]; Benchmark.BetterBenchmark.DoSomething(Int32)
       7FFD48E2EF47 add       eax,r14d
       7FFD48E2EF4A mov       [rbx],eax
       7FFD48E2EF4C add       rbp,4
       7FFD48E2EF50 dec       edi
       7FFD48E2EF52 jne       short M00_L01
M00_L02:
       7FFD48E2EF54 mov       eax,[rbx]
       7FFD48E2EF56 add       rsp,20
       7FFD48E2EF5A pop       rbx
       7FFD48E2EF5B pop       rbp
       7FFD48E2EF5C pop       rsi
       7FFD48E2EF5D pop       rdi
       7FFD48E2EF5E pop       r14
       7FFD48E2EF60 ret
M00_L03:
       7FFD48E2EF61 call      qword ptr [7FFD48FE7390]
       7FFD48E2EF67 int       3
; Total bytes of code 104
```
```assembly
; Benchmark.BetterBenchmark.DoSomething(Int32)
;     private static int DoSomething(int i) => i + i;
;                                              ^^^^^
       7FFD48E2EBF0 lea       eax,[rcx+rcx]
       7FFD48E2EBF3 ret
; Total bytes of code 4
```

