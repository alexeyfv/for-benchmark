## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
       7FFAF13E6020 push      rdi
       7FFAF13E6021 push      rsi
       7FFAF13E6022 push      rbp
       7FFAF13E6023 push      rbx
       7FFAF13E6024 sub       rsp,28
       7FFAF13E6028 mov       rsi,rcx
;         var sum = 0;
;         ^^^^^^^^^^^^
       7FFAF13E602B xor       edi,edi
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
       7FFAF13E602D xor       ebx,ebx
       7FFAF13E602F mov       rbp,[rsi+8]
       7FFAF13E6033 cmp       dword ptr [rbp+10],0
       7FFAF13E6037 jle       short M00_L01
;             sum += DoSomeThing(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L00:
       7FFAF13E6039 mov       rcx,[rsi+8]
       7FFAF13E603D cmp       ebx,[rcx+10]
       7FFAF13E6040 jae       short M00_L02
       7FFAF13E6042 mov       rcx,[rcx+8]
       7FFAF13E6046 cmp       ebx,[rcx+8]
       7FFAF13E6049 jae       short M00_L03
       7FFAF13E604B movsxd    rdx,ebx
       7FFAF13E604E mov       edx,[rcx+rdx*4+10]
       7FFAF13E6052 mov       rcx,rsi
       7FFAF13E6055 call      Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFAF13E605A add       edi,eax
       7FFAF13E605C inc       ebx
       7FFAF13E605E mov       rbp,[rsi+8]
       7FFAF13E6062 cmp       ebx,[rbp+10]
       7FFAF13E6065 jl        short M00_L00
;         return sum;
;         ^^^^^^^^^^^
M00_L01:
       7FFAF13E6067 mov       eax,edi
       7FFAF13E6069 add       rsp,28
       7FFAF13E606D pop       rbx
       7FFAF13E606E pop       rbp
       7FFAF13E606F pop       rsi
       7FFAF13E6070 pop       rdi
       7FFAF13E6071 ret
M00_L02:
       7FFAF13E6072 call      System.ThrowHelper.ThrowArgumentOutOfRange_IndexException()
       7FFAF13E6077 int       3
M00_L03:
       7FFAF13E6078 call      CORINFO_HELP_RNGCHKFAIL
       7FFAF13E607D int       3
; Total bytes of code 94
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFAF13E9570 lea       eax,[rdx+rdx]
       7FFAF13E9573 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowArgumentOutOfRange_IndexException()

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach()
       7FFAF13F6280 push      r14
       7FFAF13F6282 push      rdi
       7FFAF13F6283 push      rsi
       7FFAF13F6284 push      rbp
       7FFAF13F6285 push      rbx
       7FFAF13F6286 sub       rsp,20
       7FFAF13F628A mov       rsi,rcx
;         var sum = 0;
;         ^^^^^^^^^^^^
       7FFAF13F628D xor       edi,edi
;         foreach (var item in List)
;                              ^^^^
       7FFAF13F628F mov       rbx,[rsi+8]
       7FFAF13F6293 mov       ebp,[rbx+14]
       7FFAF13F6296 xor       r14d,r14d
       7FFAF13F6299 jmp       short M00_L01
;             sum += DoSomeThing(item);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L00:
       7FFAF13F629B mov       rcx,rsi
       7FFAF13F629E call      Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFAF13F62A3 add       edi,eax
M00_L01:
       7FFAF13F62A5 mov       rcx,rbx
       7FFAF13F62A8 cmp       ebp,[rcx+14]
       7FFAF13F62AB jne       short M00_L02
       7FFAF13F62AD cmp       r14d,[rbx+10]
       7FFAF13F62B1 jae       short M00_L03
       7FFAF13F62B3 mov       rcx,[rbx+8]
       7FFAF13F62B7 cmp       r14d,[rcx+8]
       7FFAF13F62BB jae       short M00_L06
       7FFAF13F62BD movsxd    rdx,r14d
       7FFAF13F62C0 mov       edx,[rcx+rdx*4+10]
       7FFAF13F62C4 inc       r14d
       7FFAF13F62C7 mov       ecx,1
       7FFAF13F62CC jmp       short M00_L04
M00_L02:
       7FFAF13F62CE cmp       ebp,[rbx+14]
       7FFAF13F62D1 jne       short M00_L05
M00_L03:
       7FFAF13F62D3 mov       r14d,[rbx+10]
       7FFAF13F62D7 inc       r14d
       7FFAF13F62DA xor       edx,edx
       7FFAF13F62DC xor       ecx,ecx
M00_L04:
       7FFAF13F62DE test      ecx,ecx
       7FFAF13F62E0 jne       short M00_L00
;         return sum;
;         ^^^^^^^^^^^
       7FFAF13F62E2 mov       eax,edi
       7FFAF13F62E4 add       rsp,20
       7FFAF13F62E8 pop       rbx
       7FFAF13F62E9 pop       rbp
       7FFAF13F62EA pop       rsi
       7FFAF13F62EB pop       rdi
       7FFAF13F62EC pop       r14
       7FFAF13F62EE ret
M00_L05:
       7FFAF13F62EF call      System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()
       7FFAF13F62F4 int       3
M00_L06:
       7FFAF13F62F5 call      CORINFO_HELP_RNGCHKFAIL
       7FFAF13F62FA int       3
; Total bytes of code 123
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFAF13F97F0 lea       eax,[rdx+rdx]
       7FFAF13F97F3 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         List.ForEach(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFAF1409570 push      rsi
       7FFAF1409571 sub       rsp,20
       7FFAF1409575 mov       rsi,rcx
       7FFAF1409578 mov       rcx,[rsi+8]
       7FFAF140957C mov       rdx,[rsi+10]
       7FFAF1409580 cmp       [rcx],ecx
       7FFAF1409582 call      System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFAF1409587 mov       eax,[rsi+1C]
       7FFAF140958A add       rsp,20
       7FFAF140958E pop       rsi
       7FFAF140958F ret
; Total bytes of code 32
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFAF14095C0 push      rdi
       7FFAF14095C1 push      rsi
       7FFAF14095C2 push      rbp
       7FFAF14095C3 push      rbx
       7FFAF14095C4 sub       rsp,28
       7FFAF14095C8 mov       rsi,rcx
       7FFAF14095CB mov       rdi,rdx
       7FFAF14095CE test      rdi,rdi
       7FFAF14095D1 je        short M01_L02
       7FFAF14095D3 mov       ebx,[rsi+14]
       7FFAF14095D6 xor       ebp,ebp
       7FFAF14095D8 cmp       dword ptr [rsi+10],0
       7FFAF14095DC jle       short M01_L01
M01_L00:
       7FFAF14095DE cmp       ebx,[rsi+14]
       7FFAF14095E1 jne       short M01_L01
       7FFAF14095E3 mov       rcx,[rsi+8]
       7FFAF14095E7 cmp       ebp,[rcx+8]
       7FFAF14095EA jae       short M01_L04
       7FFAF14095EC movsxd    rdx,ebp
       7FFAF14095EF mov       edx,[rcx+rdx*4+10]
       7FFAF14095F3 mov       rax,rdi
       7FFAF14095F6 mov       rcx,[rax+8]
       7FFAF14095FA call      qword ptr [rax+18]
       7FFAF14095FD inc       ebp
       7FFAF14095FF cmp       ebp,[rsi+10]
       7FFAF1409602 jl        short M01_L00
M01_L01:
       7FFAF1409604 cmp       ebx,[rsi+14]
       7FFAF1409607 jne       short M01_L03
       7FFAF1409609 add       rsp,28
       7FFAF140960D pop       rbx
       7FFAF140960E pop       rbp
       7FFAF140960F pop       rsi
       7FFAF1409610 pop       rdi
       7FFAF1409611 ret
M01_L02:
       7FFAF1409612 mov       ecx,1C
       7FFAF1409617 call      System.ThrowHelper.ThrowArgumentNullException(System.ExceptionArgument)
       7FFAF140961C int       3
M01_L03:
       7FFAF140961D call      System.ThrowHelper.ThrowInvalidOperationException_InvalidOperation_EnumFailedVersion()
       7FFAF1409622 int       3
M01_L04:
       7FFAF1409623 call      CORINFO_HELP_RNGCHKFAIL
       7FFAF1409628 int       3
; Total bytes of code 105
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         Parallel.ForEach(List, _doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFAF13F27D0 push      rsi
       7FFAF13F27D1 sub       rsp,40
       7FFAF13F27D5 mov       rsi,rcx
       7FFAF13F27D8 mov       rdx,[rsi+8]
       7FFAF13F27DC mov       r8,[rsi+10]
       7FFAF13F27E0 lea       rcx,[rsp+28]
       7FFAF13F27E5 call      System.Threading.Tasks.Parallel.ForEach[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Action`1<Int32>)
       7FFAF13F27EA mov       eax,[rsi+1C]
       7FFAF13F27ED add       rsp,40
       7FFAF13F27F1 pop       rsi
       7FFAF13F27F2 ret
; Total bytes of code 35
```
```assembly
; System.Threading.Tasks.Parallel.ForEach[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Action`1<Int32>)
       7FFAF13F2810 push      rbp
       7FFAF13F2811 push      r14
       7FFAF13F2813 push      rdi
       7FFAF13F2814 push      rsi
       7FFAF13F2815 push      rbx
       7FFAF13F2816 sub       rsp,80
       7FFAF13F281D vzeroupper
       7FFAF13F2820 lea       rbp,[rsp+0A0]
       7FFAF13F2828 xor       eax,eax
       7FFAF13F282A mov       [rbp-40],rax
       7FFAF13F282E mov       rbx,rcx
       7FFAF13F2831 mov       rsi,rdx
       7FFAF13F2834 mov       rdi,r8
       7FFAF13F2837 test      rsi,rsi
       7FFAF13F283A je        near ptr M01_L05
       7FFAF13F2840 test      rdi,rdi
       7FFAF13F2843 je        near ptr M01_L06
       7FFAF13F2849 mov       rdx,2306EDC8138
       7FFAF13F2853 mov       r14,[rdx]
       7FFAF13F2856 mov       rdx,[r14+18]
       7FFAF13F285A mov       [rbp-40],rdx
       7FFAF13F285E cmp       qword ptr [rbp-40],0
       7FFAF13F2863 jne       near ptr M01_L02
M01_L00:
       7FFAF13F2869 mov       rdx,rsi
       7FFAF13F286C mov       rcx,offset MT_System.Int32[]
       7FFAF13F2876 call      CORINFO_HELP_ISINSTANCEOFARRAY
       7FFAF13F287B test      rax,rax
       7FFAF13F287E je        near ptr M01_L03
       7FFAF13F2884 mov       [rsp+20],rdi
       7FFAF13F2889 xor       ecx,ecx
       7FFAF13F288B mov       [rsp+28],rcx
       7FFAF13F2890 mov       [rsp+30],rcx
       7FFAF13F2895 mov       [rsp+38],rcx
       7FFAF13F289A mov       [rsp+40],rcx
       7FFAF13F289F mov       [rsp+48],rcx
       7FFAF13F28A4 mov       [rsp+50],rcx
       7FFAF13F28A9 lea       rcx,[rbp-38]
       7FFAF13F28AD mov       r8,rax
       7FFAF13F28B0 mov       r9,r14
       7FFAF13F28B3 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFAF13F28BD call      System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M01_L01:
       7FFAF13F28C2 vmovdqu   xmm0,xmmword ptr [rbp-38]
       7FFAF13F28C7 vmovdqu   xmmword ptr [rbx],xmm0
       7FFAF13F28CB mov       rax,[rbp-28]
       7FFAF13F28CF mov       [rbx+10],rax
       7FFAF13F28D3 mov       rax,rbx
       7FFAF13F28D6 add       rsp,80
       7FFAF13F28DD pop       rbx
       7FFAF13F28DE pop       rsi
       7FFAF13F28DF pop       rdi
       7FFAF13F28E0 pop       r14
       7FFAF13F28E2 pop       rbp
       7FFAF13F28E3 ret
M01_L02:
       7FFAF13F28E4 mov       rdx,[rbp-40]
       7FFAF13F28E8 cmp       dword ptr [rdx+20],0
       7FFAF13F28EC setne     dl
       7FFAF13F28EF movzx     edx,dl
       7FFAF13F28F2 test      edx,edx
       7FFAF13F28F4 je        near ptr M01_L00
       7FFAF13F28FA jmp       near ptr M01_L07
M01_L03:
       7FFAF13F28FF mov       rdx,rsi
       7FFAF13F2902 mov       rcx,offset MT_System.Collections.Generic.IList`1[[System.Int32, System.Private.CoreLib]]
       7FFAF13F290C call      CORINFO_HELP_ISINSTANCEOFINTERFACE
       7FFAF13F2911 test      rax,rax
       7FFAF13F2914 je        short M01_L04
       7FFAF13F2916 mov       [rsp+20],rdi
       7FFAF13F291B xor       ecx,ecx
       7FFAF13F291D mov       [rsp+28],rcx
       7FFAF13F2922 mov       [rsp+30],rcx
       7FFAF13F2927 mov       [rsp+38],rcx
       7FFAF13F292C mov       [rsp+40],rcx
       7FFAF13F2931 mov       [rsp+48],rcx
       7FFAF13F2936 mov       [rsp+50],rcx
       7FFAF13F293B lea       rcx,[rbp-38]
       7FFAF13F293F mov       r8,rax
       7FFAF13F2942 mov       r9,r14
       7FFAF13F2945 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFAF13F294F call      System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFAF13F2954 jmp       near ptr M01_L01
M01_L04:
       7FFAF13F2959 mov       rcx,rsi
       7FFAF13F295C xor       edx,edx
       7FFAF13F295E call      System.Collections.Concurrent.Partitioner.Create[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>, System.Collections.Concurrent.EnumerablePartitionerOptions)
       7FFAF13F2963 mov       r8,rax
       7FFAF13F2966 mov       [rsp+20],rdi
       7FFAF13F296B xor       ecx,ecx
       7FFAF13F296D mov       [rsp+28],rcx
       7FFAF13F2972 mov       [rsp+30],rcx
       7FFAF13F2977 mov       [rsp+38],rcx
       7FFAF13F297C mov       [rsp+40],rcx
       7FFAF13F2981 mov       [rsp+48],rcx
       7FFAF13F2986 mov       [rsp+50],rcx
       7FFAF13F298B lea       rcx,[rbp-38]
       7FFAF13F298F mov       r9,r14
       7FFAF13F2992 mov       rdx,offset MD_System.Threading.Tasks.Parallel.PartitionerForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Concurrent.Partitioner`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFAF13F299C call      System.Threading.Tasks.Parallel.PartitionerForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Concurrent.Partitioner`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFAF13F29A1 jmp       near ptr M01_L01
M01_L05:
       7FFAF13F29A6 mov       rcx,offset MT_System.ArgumentNullException
       7FFAF13F29B0 call      CORINFO_HELP_NEWSFAST
       7FFAF13F29B5 mov       rsi,rax
       7FFAF13F29B8 mov       ecx,3C3
       7FFAF13F29BD mov       rdx,7FFAF14B88D0
       7FFAF13F29C7 call      CORINFO_HELP_STRCNS
       7FFAF13F29CC mov       rdx,rax
       7FFAF13F29CF mov       rcx,rsi
       7FFAF13F29D2 call      System.ArgumentNullException..ctor(System.String)
       7FFAF13F29D7 mov       rcx,rsi
       7FFAF13F29DA call      CORINFO_HELP_THROW
M01_L06:
       7FFAF13F29DF mov       rcx,offset MT_System.ArgumentNullException
       7FFAF13F29E9 call      CORINFO_HELP_NEWSFAST
       7FFAF13F29EE mov       rsi,rax
       7FFAF13F29F1 mov       ecx,38B
       7FFAF13F29F6 mov       rdx,7FFAF14B88D0
       7FFAF13F2A00 call      CORINFO_HELP_STRCNS
       7FFAF13F2A05 mov       rdx,rax
       7FFAF13F2A08 mov       rcx,rsi
       7FFAF13F2A0B call      System.ArgumentNullException..ctor(System.String)
       7FFAF13F2A10 mov       rcx,rsi
       7FFAF13F2A13 call      CORINFO_HELP_THROW
M01_L07:
       7FFAF13F2A18 lea       rcx,[rbp-40]
       7FFAF13F2A1C call      System.Threading.CancellationToken.ThrowOperationCanceledException()
       7FFAF13F2A21 int       3
; Total bytes of code 530
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         List.AsParallel().ForAll(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFAF13E8840 push      rsi
       7FFAF13E8841 sub       rsp,20
       7FFAF13E8845 mov       rsi,rcx
       7FFAF13E8848 mov       rcx,[rsi+8]
       7FFAF13E884C call      System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFAF13E8851 mov       rcx,rax
       7FFAF13E8854 mov       rdx,[rsi+10]
       7FFAF13E8858 call      System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFAF13E885D mov       eax,[rsi+1C]
       7FFAF13E8860 add       rsp,20
       7FFAF13E8864 pop       rsi
       7FFAF13E8865 ret
; Total bytes of code 38
```
```assembly
; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFAF13E8880 push      rdi
       7FFAF13E8881 push      rsi
       7FFAF13E8882 push      rbp
       7FFAF13E8883 push      rbx
       7FFAF13E8884 sub       rsp,88
       7FFAF13E888B vzeroupper
       7FFAF13E888E xor       eax,eax
       7FFAF13E8890 mov       [rsp+28],rax
       7FFAF13E8895 vxorps    xmm4,xmm4,xmm4
       7FFAF13E8899 vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFAF13E889F vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFAF13E88A5 vmovdqa   xmmword ptr [rsp+50],xmm4
       7FFAF13E88AB vmovdqa   xmmword ptr [rsp+60],xmm4
       7FFAF13E88B1 vmovdqa   xmmword ptr [rsp+70],xmm4
       7FFAF13E88B7 mov       [rsp+80],rax
       7FFAF13E88BF mov       rbx,rcx
       7FFAF13E88C2 test      rbx,rbx
       7FFAF13E88C5 je        near ptr M01_L00
       7FFAF13E88CB mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFAF13E88D5 call      CORINFO_HELP_NEWSFAST
       7FFAF13E88DA mov       rbp,rax
       7FFAF13E88DD lea       rcx,[rsp+58]
       7FFAF13E88E2 call      System.Linq.Parallel.QuerySettings.get_Empty()
       7FFAF13E88E7 vmovdqu   xmm0,xmmword ptr [rsp+58]
       7FFAF13E88ED vmovdqu   xmmword ptr [rsp+28],xmm0
       7FFAF13E88F3 vmovdqu   xmm0,xmmword ptr [rsp+68]
       7FFAF13E88F9 vmovdqu   xmmword ptr [rsp+38],xmm0
       7FFAF13E88FF vmovdqu   xmm0,xmmword ptr [rsp+78]
       7FFAF13E8905 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFAF13E890B lea       rdi,[rbp+8]
       7FFAF13E890F lea       rsi,[rsp+28]
       7FFAF13E8914 call      CORINFO_HELP_ASSIGN_BYREF
       7FFAF13E8919 call      CORINFO_HELP_ASSIGN_BYREF
       7FFAF13E891E mov       ecx,4
       7FFAF13E8923 rep movsq
       7FFAF13E8926 lea       rcx,[rbp+38]
       7FFAF13E892A mov       rdx,rbx
       7FFAF13E892D call      CORINFO_HELP_ASSIGN_REF
       7FFAF13E8932 mov       rax,rbp
       7FFAF13E8935 add       rsp,88
       7FFAF13E893C pop       rbx
       7FFAF13E893D pop       rbp
       7FFAF13E893E pop       rsi
       7FFAF13E893F pop       rdi
       7FFAF13E8940 ret
M01_L00:
       7FFAF13E8941 mov       rcx,offset MT_System.ArgumentNullException
       7FFAF13E894B call      CORINFO_HELP_NEWSFAST
       7FFAF13E8950 mov       rsi,rax
       7FFAF13E8953 mov       ecx,6F1
       7FFAF13E8958 mov       rdx,7FFAF14A88C8
       7FFAF13E8962 call      CORINFO_HELP_STRCNS
       7FFAF13E8967 mov       rdx,rax
       7FFAF13E896A mov       rcx,rsi
       7FFAF13E896D call      System.ArgumentNullException..ctor(System.String)
       7FFAF13E8972 mov       rcx,rsi
       7FFAF13E8975 call      CORINFO_HELP_THROW
       7FFAF13E897A int       3
; Total bytes of code 251
```
```assembly
; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFAF13E8E90 push      r15
       7FFAF13E8E92 push      r14
       7FFAF13E8E94 push      rdi
       7FFAF13E8E95 push      rsi
       7FFAF13E8E96 push      rbp
       7FFAF13E8E97 push      rbx
       7FFAF13E8E98 sub       rsp,58
       7FFAF13E8E9C vzeroupper
       7FFAF13E8E9F xor       eax,eax
       7FFAF13E8EA1 mov       [rsp+28],rax
       7FFAF13E8EA6 vxorps    xmm4,xmm4,xmm4
       7FFAF13E8EAA vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFAF13E8EB0 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFAF13E8EB6 mov       [rsp+50],rax
       7FFAF13E8EBB mov       rsi,rcx
       7FFAF13E8EBE mov       rbx,rdx
       7FFAF13E8EC1 test      rsi,rsi
       7FFAF13E8EC4 je        near ptr M02_L00
       7FFAF13E8ECA test      rbx,rbx
       7FFAF13E8ECD je        near ptr M02_L01
       7FFAF13E8ED3 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFAF13E8EDD call      CORINFO_HELP_NEWSFAST
       7FFAF13E8EE2 mov       rbp,rax
       7FFAF13E8EE5 mov       rcx,rsi
       7FFAF13E8EE8 call      System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFAF13E8EED mov       r14,rax
       7FFAF13E8EF0 movzx     ecx,byte ptr [r14+38]
       7FFAF13E8EF5 vmovdqu   xmm0,xmmword ptr [r14+8]
       7FFAF13E8EFB vmovdqu   xmmword ptr [rsp+28],xmm0
       7FFAF13E8F01 vmovdqu   xmm0,xmmword ptr [r14+18]
       7FFAF13E8F07 vmovdqu   xmmword ptr [rsp+38],xmm0
       7FFAF13E8F0D vmovdqu   xmm0,xmmword ptr [r14+28]
       7FFAF13E8F13 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFAF13E8F19 movzx     r15d,cl
       7FFAF13E8F1D mov       byte ptr [rbp+48],3
       7FFAF13E8F21 lea       rdi,[rbp+8]
       7FFAF13E8F25 lea       rsi,[rsp+28]
       7FFAF13E8F2A call      CORINFO_HELP_ASSIGN_BYREF
       7FFAF13E8F2F call      CORINFO_HELP_ASSIGN_BYREF
       7FFAF13E8F34 mov       ecx,4
       7FFAF13E8F39 rep movsq
       7FFAF13E8F3C mov       [rbp+38],r15b
       7FFAF13E8F40 lea       rcx,[rbp+40]
       7FFAF13E8F44 mov       rdx,r14
       7FFAF13E8F47 call      CORINFO_HELP_ASSIGN_REF
       7FFAF13E8F4C lea       rcx,[rbp+50]
       7FFAF13E8F50 mov       rdx,rbx
       7FFAF13E8F53 call      CORINFO_HELP_ASSIGN_REF
       7FFAF13E8F58 mov       rcx,rbp
       7FFAF13E8F5B add       rsp,58
       7FFAF13E8F5F pop       rbx
       7FFAF13E8F60 pop       rbp
       7FFAF13E8F61 pop       rsi
       7FFAF13E8F62 pop       rdi
       7FFAF13E8F63 pop       r14
       7FFAF13E8F65 pop       r15
       7FFAF13E8F67 jmp       near ptr System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
M02_L00:
       7FFAF13E8F6C mov       rcx,offset MT_System.ArgumentNullException
       7FFAF13E8F76 call      CORINFO_HELP_NEWSFAST
       7FFAF13E8F7B mov       rsi,rax
       7FFAF13E8F7E mov       ecx,6F1
       7FFAF13E8F83 mov       rdx,7FFAF14A88C8
       7FFAF13E8F8D call      CORINFO_HELP_STRCNS
       7FFAF13E8F92 mov       rdx,rax
       7FFAF13E8F95 mov       rcx,rsi
       7FFAF13E8F98 call      System.ArgumentNullException..ctor(System.String)
       7FFAF13E8F9D mov       rcx,rsi
       7FFAF13E8FA0 call      CORINFO_HELP_THROW
M02_L01:
       7FFAF13E8FA5 mov       rcx,offset MT_System.ArgumentNullException
       7FFAF13E8FAF call      CORINFO_HELP_NEWSFAST
       7FFAF13E8FB4 mov       rsi,rax
       7FFAF13E8FB7 mov       ecx,733
       7FFAF13E8FBC mov       rdx,7FFAF14A88C8
       7FFAF13E8FC6 call      CORINFO_HELP_STRCNS
       7FFAF13E8FCB mov       rdx,rax
       7FFAF13E8FCE mov       rcx,rsi
       7FFAF13E8FD1 call      System.ArgumentNullException..ctor(System.String)
       7FFAF13E8FD6 mov       rcx,rsi
       7FFAF13E8FD9 call      CORINFO_HELP_THROW
       7FFAF13E8FDE int       3
; Total bytes of code 335
```

## .NET 6.0.33 (6.0.3324.36610), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
       7FFAF13F6680 push      r14
       7FFAF13F6682 push      rdi
       7FFAF13F6683 push      rsi
       7FFAF13F6684 push      rbp
       7FFAF13F6685 push      rbx
       7FFAF13F6686 sub       rsp,20
       7FFAF13F668A mov       rsi,rcx
;         var sum = 0;
;         ^^^^^^^^^^^^
       7FFAF13F668D xor       edi,edi
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
       7FFAF13F668F mov       rdx,[rsi+8]
       7FFAF13F6693 test      rdx,rdx
       7FFAF13F6696 je        short M00_L02
       7FFAF13F6698 mov       rcx,[rdx+8]
       7FFAF13F669C mov       ebx,[rdx+10]
       7FFAF13F669F test      rcx,rcx
       7FFAF13F66A2 jne       short M00_L00
       7FFAF13F66A4 test      ebx,ebx
       7FFAF13F66A6 jne       short M00_L06
       7FFAF13F66A8 xor       ebp,ebp
       7FFAF13F66AA xor       ebx,ebx
       7FFAF13F66AC jmp       short M00_L01
M00_L00:
       7FFAF13F66AE mov       edx,[rcx+8]
       7FFAF13F66B1 mov       eax,ebx
       7FFAF13F66B3 cmp       rdx,rax
       7FFAF13F66B6 jb        short M00_L06
       7FFAF13F66B8 add       rcx,10
       7FFAF13F66BC mov       rbp,rcx
M00_L01:
       7FFAF13F66BF jmp       short M00_L03
M00_L02:
       7FFAF13F66C1 xor       ebp,ebp
       7FFAF13F66C3 xor       ebx,ebx
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
M00_L03:
       7FFAF13F66C5 xor       r14d,r14d
       7FFAF13F66C8 test      ebx,ebx
       7FFAF13F66CA jle       short M00_L05
;             sum += DoSomeThing(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
M00_L04:
       7FFAF13F66CC movsxd    rdx,r14d
       7FFAF13F66CF mov       edx,[rbp+rdx*4]
       7FFAF13F66D3 mov       rcx,rsi
       7FFAF13F66D6 call      Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFAF13F66DB add       edi,eax
       7FFAF13F66DD inc       r14d
       7FFAF13F66E0 cmp       r14d,ebx
       7FFAF13F66E3 jl        short M00_L04
;         return sum;
;         ^^^^^^^^^^^
M00_L05:
       7FFAF13F66E5 mov       eax,edi
       7FFAF13F66E7 add       rsp,20
       7FFAF13F66EB pop       rbx
       7FFAF13F66EC pop       rbp
       7FFAF13F66ED pop       rsi
       7FFAF13F66EE pop       rdi
       7FFAF13F66EF pop       r14
       7FFAF13F66F1 ret
M00_L06:
       7FFAF13F66F2 call      System.ThrowHelper.ThrowArgumentOutOfRangeException()
       7FFAF13F66F7 int       3
; Total bytes of code 120
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFAF13F9BD0 lea       eax,[rdx+rdx]
       7FFAF13F9BD3 ret
; Total bytes of code 4
```
**Method was not JITted yet.**
System.ThrowHelper.ThrowArgumentOutOfRangeException()

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
;         var sum = 0;
;         ^^^^^^^^^^^^
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
;             sum += DoSomeThing(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2D779640 push      rdi
       7FFB2D779641 push      rsi
       7FFB2D779642 push      rbx
       7FFB2D779643 sub       rsp,20
       7FFB2D779647 mov       rbx,rcx
       7FFB2D77964A xor       esi,esi
       7FFB2D77964C xor       edi,edi
       7FFB2D77964E mov       rcx,[rbx+8]
       7FFB2D779652 cmp       dword ptr [rcx+10],0
       7FFB2D779656 jle       short M00_L01
M00_L00:
       7FFB2D779658 mov       rcx,[rbx+8]
       7FFB2D77965C cmp       edi,[rcx+10]
       7FFB2D77965F jae       short M00_L02
       7FFB2D779661 mov       rcx,[rcx+8]
       7FFB2D779665 cmp       edi,[rcx+8]
       7FFB2D779668 jae       short M00_L03
       7FFB2D77966A mov       edx,edi
       7FFB2D77966C mov       edx,[rcx+rdx*4+10]
       7FFB2D779670 mov       rcx,rbx
       7FFB2D779673 call      qword ptr [7FFB2D9EEE50]; Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFB2D779679 add       esi,eax
       7FFB2D77967B inc       edi
       7FFB2D77967D mov       rax,[rbx+8]
       7FFB2D779681 cmp       edi,[rax+10]
       7FFB2D779684 jl        short M00_L00
M00_L01:
       7FFB2D779686 mov       eax,esi
       7FFB2D779688 add       rsp,20
       7FFB2D77968C pop       rbx
       7FFB2D77968D pop       rsi
       7FFB2D77968E pop       rdi
       7FFB2D77968F ret
M00_L02:
       7FFB2D779690 call      qword ptr [7FFB2D9E5878]
       7FFB2D779696 int       3
M00_L03:
       7FFB2D779697 call      CORINFO_HELP_RNGCHKFAIL
       7FFB2D77969C int       3
; Total bytes of code 93
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFB2D7793A0 lea       eax,[rdx+rdx]
       7FFB2D7793A3 ret
; Total bytes of code 4
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         List.ForEach(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2D799400 push      rbx
       7FFB2D799401 sub       rsp,20
       7FFB2D799405 mov       rbx,rcx
       7FFB2D799408 mov       rcx,[rbx+8]
       7FFB2D79940C mov       rdx,[rbx+10]
       7FFB2D799410 cmp       [rcx],ecx
       7FFB2D799412 call      qword ptr [7FFB2D8AF000]; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFB2D799418 mov       eax,[rbx+1C]
       7FFB2D79941B add       rsp,20
       7FFB2D79941F pop       rbx
       7FFB2D799420 ret
; Total bytes of code 33
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFB2D799440 push      r14
       7FFB2D799442 push      rdi
       7FFB2D799443 push      rsi
       7FFB2D799444 push      rbp
       7FFB2D799445 push      rbx
       7FFB2D799446 sub       rsp,20
       7FFB2D79944A mov       rbx,rcx
       7FFB2D79944D mov       rsi,rdx
       7FFB2D799450 test      rsi,rsi
       7FFB2D799453 je        near ptr M01_L04
       7FFB2D799459 mov       edi,[rbx+14]
       7FFB2D79945C xor       ebp,ebp
       7FFB2D79945E cmp       dword ptr [rbx+10],0
       7FFB2D799462 jle       short M01_L03
       7FFB2D799464 mov       r14,[rsi+18]
       7FFB2D799468 mov       rcx,7FFB2DA0AE80
       7FFB2D799472 cmp       r14,rcx
       7FFB2D799475 jne       short M01_L01
M01_L00:
       7FFB2D799477 cmp       edi,[rbx+14]
       7FFB2D79947A jne       short M01_L03
       7FFB2D79947C mov       rcx,[rbx+8]
       7FFB2D799480 cmp       ebp,[rcx+8]
       7FFB2D799483 jae       short M01_L07
       7FFB2D799485 mov       eax,ebp
       7FFB2D799487 mov       edx,[rcx+rax*4+10]
       7FFB2D79948B mov       rax,[rsi+8]
       7FFB2D79948F add       edx,edx
       7FFB2D799491 add       [rax+1C],edx
       7FFB2D799494 inc       ebp
       7FFB2D799496 cmp       ebp,[rbx+10]
       7FFB2D799499 jl        short M01_L00
       7FFB2D79949B jmp       short M01_L03
M01_L01:
       7FFB2D79949D cmp       edi,[rbx+14]
       7FFB2D7994A0 jne       short M01_L03
       7FFB2D7994A2 mov       rcx,[rbx+8]
       7FFB2D7994A6 cmp       ebp,[rcx+8]
       7FFB2D7994A9 jae       short M01_L07
       7FFB2D7994AB mov       eax,ebp
       7FFB2D7994AD mov       edx,[rcx+rax*4+10]
       7FFB2D7994B1 mov       rcx,7FFB2DA0AE80
       7FFB2D7994BB cmp       r14,rcx
       7FFB2D7994BE jne       short M01_L05
       7FFB2D7994C0 mov       rax,[rsi+8]
       7FFB2D7994C4 lea       ecx,[rdx+rdx]
       7FFB2D7994C7 add       [rax+1C],ecx
M01_L02:
       7FFB2D7994CA inc       ebp
       7FFB2D7994CC cmp       ebp,[rbx+10]
       7FFB2D7994CF jl        short M01_L01
M01_L03:
       7FFB2D7994D1 cmp       edi,[rbx+14]
       7FFB2D7994D4 jne       short M01_L06
       7FFB2D7994D6 add       rsp,20
       7FFB2D7994DA pop       rbx
       7FFB2D7994DB pop       rbp
       7FFB2D7994DC pop       rsi
       7FFB2D7994DD pop       rdi
       7FFB2D7994DE pop       r14
       7FFB2D7994E0 ret
M01_L04:
       7FFB2D7994E1 mov       ecx,1C
       7FFB2D7994E6 call      qword ptr [7FFB2DA05B18]
       7FFB2D7994EC int       3
M01_L05:
       7FFB2D7994ED mov       rcx,[rsi+8]
       7FFB2D7994F1 call      qword ptr [rsi+18]
       7FFB2D7994F4 jmp       short M01_L02
M01_L06:
       7FFB2D7994F6 call      qword ptr [7FFB2DA05E00]
       7FFB2D7994FC int       3
M01_L07:
       7FFB2D7994FD call      CORINFO_HELP_RNGCHKFAIL
       7FFB2D799502 int       3
; Total bytes of code 195
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         Parallel.ForEach(List, _doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2D79A4C0 push      rbp
       7FFB2D79A4C1 push      r14
       7FFB2D79A4C3 push      rdi
       7FFB2D79A4C4 push      rsi
       7FFB2D79A4C5 push      rbx
       7FFB2D79A4C6 sub       rsp,80
       7FFB2D79A4CD lea       rbp,[rsp+0A0]
       7FFB2D79A4D5 xor       eax,eax
       7FFB2D79A4D7 mov       [rbp-40],rax
       7FFB2D79A4DB mov       rbx,rcx
       7FFB2D79A4DE mov       rsi,[rbx+8]
       7FFB2D79A4E2 mov       rdi,[rbx+10]
       7FFB2D79A4E6 test      rsi,rsi
       7FFB2D79A4E9 je        near ptr M00_L03
       7FFB2D79A4EF test      rdi,rdi
       7FFB2D79A4F2 je        near ptr M00_L04
       7FFB2D79A4F8 mov       rdx,21C4B406E38
       7FFB2D79A502 mov       r14,[rdx]
       7FFB2D79A505 mov       rdx,[r14+18]
       7FFB2D79A509 mov       [rbp-40],rdx
       7FFB2D79A50D cmp       qword ptr [rbp-40],0
       7FFB2D79A512 jne       short M00_L02
M00_L00:
       7FFB2D79A514 mov       rdx,rsi
       7FFB2D79A517 mov       rcx,offset MT_System.Int32[]
       7FFB2D79A521 call      qword ptr [7FFB2D754330]; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFB2D79A527 test      rax,rax
       7FFB2D79A52A jne       near ptr M00_L05
       7FFB2D79A530 mov       r8,rsi
       7FFB2D79A533 mov       [rsp+20],rdi
       7FFB2D79A538 xor       ecx,ecx
       7FFB2D79A53A mov       [rsp+28],rcx
       7FFB2D79A53F mov       [rsp+30],rcx
       7FFB2D79A544 mov       [rsp+38],rcx
       7FFB2D79A549 mov       [rsp+40],rcx
       7FFB2D79A54E mov       [rsp+48],rcx
       7FFB2D79A553 mov       [rsp+50],rcx
       7FFB2D79A558 lea       rcx,[rbp-38]
       7FFB2D79A55C mov       r9,r14
       7FFB2D79A55F mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFB2D79A569 call      qword ptr [7FFB2DBC6E80]; System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M00_L01:
       7FFB2D79A56F mov       eax,[rbx+1C]
       7FFB2D79A572 add       rsp,80
       7FFB2D79A579 pop       rbx
       7FFB2D79A57A pop       rsi
       7FFB2D79A57B pop       rdi
       7FFB2D79A57C pop       r14
       7FFB2D79A57E pop       rbp
       7FFB2D79A57F ret
M00_L02:
       7FFB2D79A580 mov       rdx,[rbp-40]
       7FFB2D79A584 cmp       dword ptr [rdx+20],0
       7FFB2D79A588 je        short M00_L00
       7FFB2D79A58A lea       rcx,[rbp-40]
       7FFB2D79A58E call      qword ptr [7FFB2D9BD740]
       7FFB2D79A594 int       3
M00_L03:
       7FFB2D79A595 mov       ecx,3C3
       7FFB2D79A59A mov       rdx,7FFB2DBB4AF8
       7FFB2D79A5A4 call      CORINFO_HELP_STRCNS
       7FFB2D79A5A9 mov       rcx,rax
       7FFB2D79A5AC call      qword ptr [7FFB2D876790]
       7FFB2D79A5B2 int       3
M00_L04:
       7FFB2D79A5B3 mov       ecx,38B
       7FFB2D79A5B8 mov       rdx,7FFB2DBB4AF8
       7FFB2D79A5C2 call      CORINFO_HELP_STRCNS
       7FFB2D79A5C7 mov       rcx,rax
       7FFB2D79A5CA call      qword ptr [7FFB2D876790]
       7FFB2D79A5D0 int       3
M00_L05:
       7FFB2D79A5D1 mov       [rsp+20],rdi
       7FFB2D79A5D6 xor       ecx,ecx
       7FFB2D79A5D8 mov       [rsp+28],rcx
       7FFB2D79A5DD mov       [rsp+30],rcx
       7FFB2D79A5E2 mov       [rsp+38],rcx
       7FFB2D79A5E7 mov       [rsp+40],rcx
       7FFB2D79A5EC mov       [rsp+48],rcx
       7FFB2D79A5F1 mov       [rsp+50],rcx
       7FFB2D79A5F6 lea       rcx,[rbp-38]
       7FFB2D79A5FA mov       r8,rax
       7FFB2D79A5FD mov       r9,r14
       7FFB2D79A600 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.Object, System.Private.CoreLib]](Int32[], System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFB2D79A60A call      qword ptr [7FFB2DBC6EC8]
       7FFB2D79A610 jmp       near ptr M00_L01
; Total bytes of code 341
```
```assembly
; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFB2D792D40 push      rsi
       7FFB2D792D41 push      rbx
       7FFB2D792D42 test      rdx,rdx
       7FFB2D792D45 je        short M01_L00
       7FFB2D792D47 mov       rax,[rdx]
       7FFB2D792D4A cmp       rax,rcx
       7FFB2D792D4D jne       short M01_L01
M01_L00:
       7FFB2D792D4F mov       rax,rdx
       7FFB2D792D52 pop       rbx
       7FFB2D792D53 pop       rsi
       7FFB2D792D54 ret
M01_L01:
       7FFB2D792D55 mov       r8,21C4B400B50
       7FFB2D792D5F mov       r8,[r8]
       7FFB2D792D62 add       r8,10
       7FFB2D792D66 rorx      r10,rax,20
       7FFB2D792D6C xor       r10,rcx
       7FFB2D792D6F mov       r9,9E3779B97F4A7C15
       7FFB2D792D79 imul      r10,r9
       7FFB2D792D7D mov       r9d,[r8]
       7FFB2D792D80 shrx      r10,r10,r9
       7FFB2D792D85 xor       r9d,r9d
M01_L02:
       7FFB2D792D88 lea       r11d,[r10+1]
       7FFB2D792D8C movsxd    r11,r11d
       7FFB2D792D8F lea       r11,[r11+r11*2]
       7FFB2D792D93 lea       r11,[r8+r11*8]
       7FFB2D792D97 mov       ebx,[r11]
       7FFB2D792D9A mov       rsi,[r11+8]
       7FFB2D792D9E and       ebx,0FFFFFFFE
       7FFB2D792DA1 cmp       rsi,rax
       7FFB2D792DA4 jne       short M01_L03
       7FFB2D792DA6 mov       rsi,rcx
       7FFB2D792DA9 xor       rsi,[r11+10]
       7FFB2D792DAD cmp       rsi,1
       7FFB2D792DB1 jbe       short M01_L04
M01_L03:
       7FFB2D792DB3 test      ebx,ebx
       7FFB2D792DB5 je        short M01_L06
       7FFB2D792DB7 inc       r9d
       7FFB2D792DBA add       r10d,r9d
       7FFB2D792DBD and       r10d,[r8+4]
       7FFB2D792DC1 cmp       r9d,8
       7FFB2D792DC5 jl        short M01_L02
       7FFB2D792DC7 jmp       short M01_L06
M01_L04:
       7FFB2D792DC9 cmp       ebx,[r11]
       7FFB2D792DCC jne       short M01_L06
M01_L05:
       7FFB2D792DCE cmp       esi,1
       7FFB2D792DD1 je        near ptr M01_L00
       7FFB2D792DD7 test      esi,esi
       7FFB2D792DD9 jne       short M01_L07
       7FFB2D792DDB xor       edx,edx
       7FFB2D792DDD jmp       near ptr M01_L00
M01_L06:
       7FFB2D792DE2 mov       esi,2
       7FFB2D792DE7 jmp       short M01_L05
M01_L07:
       7FFB2D792DE9 pop       rbx
       7FFB2D792DEA pop       rsi
       7FFB2D792DEB jmp       near ptr System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny_NoCacheLookup(Void*, System.Object)
; Total bytes of code 176
```
```assembly
; System.Threading.Tasks.Parallel.ForEachWorker[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]](System.Collections.Generic.IList`1<Int32>, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Action`3<Int32,System.Threading.Tasks.ParallelLoopState,Int64>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`5<Int32,System.Threading.Tasks.ParallelLoopState,Int64,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFB2D79AB40 push      rbp
       7FFB2D79AB41 push      r15
       7FFB2D79AB43 push      r14
       7FFB2D79AB45 push      r13
       7FFB2D79AB47 push      r12
       7FFB2D79AB49 push      rdi
       7FFB2D79AB4A push      rsi
       7FFB2D79AB4B push      rbx
       7FFB2D79AB4C sub       rsp,38
       7FFB2D79AB50 lea       rbp,[rsp+70]
       7FFB2D79AB55 mov       [rbp-40],rdx
       7FFB2D79AB59 mov       rsi,rcx
       7FFB2D79AB5C mov       rbx,rdx
       7FFB2D79AB5F mov       r14,r8
       7FFB2D79AB62 mov       rdi,r9
       7FFB2D79AB65 mov       rcx,[rbx+10]
       7FFB2D79AB69 mov       rcx,[rcx+18]
       7FFB2D79AB6D test      rcx,rcx
       7FFB2D79AB70 je        short M02_L00
       7FFB2D79AB72 jmp       short M02_L01
M02_L00:
       7FFB2D79AB74 mov       rcx,rbx
       7FFB2D79AB77 mov       rdx,7FFB2DBD1140
       7FFB2D79AB81 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFB2D79AB86 mov       rcx,rax
M02_L01:
       7FFB2D79AB89 call      CORINFO_HELP_NEWSFAST
       7FFB2D79AB8E mov       r15,rax
       7FFB2D79AB91 lea       rcx,[r15+8]
       7FFB2D79AB95 mov       rdx,[rbp+30]
       7FFB2D79AB99 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79AB9E lea       rcx,[r15+10]
       7FFB2D79ABA2 mov       rdx,r14
       7FFB2D79ABA5 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79ABAA lea       rcx,[r15+18]
       7FFB2D79ABAE mov       rdx,[rbp+38]
       7FFB2D79ABB2 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79ABB7 lea       rcx,[r15+20]
       7FFB2D79ABBB mov       rdx,[rbp+40]
       7FFB2D79ABBF call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79ABC4 lea       rcx,[r15+28]
       7FFB2D79ABC8 mov       rdx,[rbp+48]
       7FFB2D79ABCC call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79ABD1 lea       rcx,[r15+30]
       7FFB2D79ABD5 mov       rdx,[rbp+50]
       7FFB2D79ABD9 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79ABDE cmp       qword ptr [r15+8],0
       7FFB2D79ABE3 je        near ptr M02_L03
       7FFB2D79ABE9 mov       rcx,[r15+10]
       7FFB2D79ABED mov       rax,offset MT_System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]]
       7FFB2D79ABF7 cmp       [rcx],rax
       7FFB2D79ABFA jne       near ptr M02_L15
       7FFB2D79AC00 mov       ebx,[rcx+10]
M02_L02:
       7FFB2D79AC03 mov       rcx,offset MT_System.Action`1[[System.Int32, System.Private.CoreLib]]
       7FFB2D79AC0D call      CORINFO_HELP_NEWSFAST
       7FFB2D79AC12 mov       r14,rax
       7FFB2D79AC15 lea       rcx,[r14+8]
       7FFB2D79AC19 mov       rdx,r15
       7FFB2D79AC1C call      CORINFO_HELP_ASSIGN_REF
       7FFB2D79AC21 mov       rcx,7FFB2DBC2FD0
       7FFB2D79AC2B mov       [r14+18],rcx
       7FFB2D79AC2F mov       [rbp+30],rdi
       7FFB2D79AC33 mov       [rbp+38],r14
       7FFB2D79AC37 xor       ecx,ecx
       7FFB2D79AC39 mov       [rbp+40],rcx
       7FFB2D79AC3D mov       [rbp+48],rcx
       7FFB2D79AC41 mov       [rbp+50],rcx
       7FFB2D79AC45 mov       [rbp+58],rcx
       7FFB2D79AC49 mov       rcx,rsi
       7FFB2D79AC4C mov       r9d,ebx
       7FFB2D79AC4F mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFB2D79AC59 xor       r8d,r8d
       7FFB2D79AC5C add       rsp,38
       7FFB2D79AC60 pop       rbx
       7FFB2D79AC61 pop       rsi
       7FFB2D79AC62 pop       rdi
       7FFB2D79AC63 pop       r12
       7FFB2D79AC65 pop       r13
       7FFB2D79AC67 pop       r14
       7FFB2D79AC69 pop       r15
       7FFB2D79AC6B pop       rbp
       7FFB2D79AC6C jmp       qword ptr [7FFB2DBC7138]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L03:
       7FFB2D79AC72 cmp       qword ptr [r15+18],0
       7FFB2D79AC77 je        near ptr M02_L04
       7FFB2D79AC7D mov       rcx,offset MT_System.Action`2[[System.Int32, System.Private.CoreLib],[System.Threading.Tasks.ParallelLoopState, System.Threading.Tasks.Parallel]]
       7FFB2D79AC87 call      CORINFO_HELP_NEWSFAST
       7FFB2D79AC8C mov       rbx,rax
       7FFB2D79AC8F mov       rcx,[r15+10]
       7FFB2D79AC93 mov       r11,7FFB2D610590
       7FFB2D79AC9D call      qword ptr [r11]
       7FFB2D79ACA0 mov       r14d,eax
       7FFB2D79ACA3 mov       rcx,rbx
       7FFB2D79ACA6 mov       rdx,r15
       7FFB2D79ACA9 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__1(Int32, System.Threading.Tasks.ParallelLoopState)
       7FFB2D79ACB3 call      qword ptr [7FFB2D754210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFB2D79ACB9 mov       [rbp+30],rdi
       7FFB2D79ACBD xor       ecx,ecx
       7FFB2D79ACBF mov       [rbp+38],rcx
       7FFB2D79ACC3 mov       [rbp+40],rbx
       7FFB2D79ACC7 mov       [rbp+48],rcx
       7FFB2D79ACCB mov       [rbp+50],rcx
       7FFB2D79ACCF mov       [rbp+58],rcx
       7FFB2D79ACD3 mov       rcx,rsi
       7FFB2D79ACD6 mov       r9d,r14d
       7FFB2D79ACD9 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFB2D79ACE3 xor       r8d,r8d
       7FFB2D79ACE6 add       rsp,38
       7FFB2D79ACEA pop       rbx
       7FFB2D79ACEB pop       rsi
       7FFB2D79ACEC pop       rdi
       7FFB2D79ACED pop       r12
       7FFB2D79ACEF pop       r13
       7FFB2D79ACF1 pop       r14
       7FFB2D79ACF3 pop       r15
       7FFB2D79ACF5 pop       rbp
       7FFB2D79ACF6 jmp       qword ptr [7FFB2DBC7138]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L04:
       7FFB2D79ACFC cmp       qword ptr [r15+20],0
       7FFB2D79AD01 je        near ptr M02_L05
       7FFB2D79AD07 mov       rcx,offset MT_System.Action`2[[System.Int32, System.Private.CoreLib],[System.Threading.Tasks.ParallelLoopState, System.Threading.Tasks.Parallel]]
       7FFB2D79AD11 call      CORINFO_HELP_NEWSFAST
       7FFB2D79AD16 mov       rbx,rax
       7FFB2D79AD19 mov       rcx,[r15+10]
       7FFB2D79AD1D mov       r11,7FFB2D610588
       7FFB2D79AD27 call      qword ptr [r11]
       7FFB2D79AD2A mov       r14d,eax
       7FFB2D79AD2D mov       rcx,rbx
       7FFB2D79AD30 mov       rdx,r15
       7FFB2D79AD33 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__2(Int32, System.Threading.Tasks.ParallelLoopState)
       7FFB2D79AD3D call      qword ptr [7FFB2D754210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFB2D79AD43 mov       [rbp+30],rdi
       7FFB2D79AD47 xor       ecx,ecx
       7FFB2D79AD49 mov       [rbp+38],rcx
       7FFB2D79AD4D mov       [rbp+40],rbx
       7FFB2D79AD51 mov       [rbp+48],rcx
       7FFB2D79AD55 mov       [rbp+50],rcx
       7FFB2D79AD59 mov       [rbp+58],rcx
       7FFB2D79AD5D mov       rcx,rsi
       7FFB2D79AD60 mov       r9d,r14d
       7FFB2D79AD63 mov       rdx,offset MD_System.Threading.Tasks.Parallel.ForWorker[[System.Object, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.Object,System.Object>, System.Func`1<System.Object>, System.Action`1<System.Object>)
       7FFB2D79AD6D xor       r8d,r8d
       7FFB2D79AD70 add       rsp,38
       7FFB2D79AD74 pop       rbx
       7FFB2D79AD75 pop       rsi
       7FFB2D79AD76 pop       rdi
       7FFB2D79AD77 pop       r12
       7FFB2D79AD79 pop       r13
       7FFB2D79AD7B pop       r14
       7FFB2D79AD7D pop       r15
       7FFB2D79AD7F pop       rbp
       7FFB2D79AD80 jmp       qword ptr [7FFB2DBC7138]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L05:
       7FFB2D79AD86 cmp       qword ptr [r15+28],0
       7FFB2D79AD8B je        near ptr M02_L10
       7FFB2D79AD91 mov       rcx,[rbx+10]
       7FFB2D79AD95 mov       rcx,[rcx+20]
       7FFB2D79AD99 test      rcx,rcx
       7FFB2D79AD9C je        short M02_L06
       7FFB2D79AD9E jmp       short M02_L07
M02_L06:
       7FFB2D79ADA0 mov       rcx,rbx
       7FFB2D79ADA3 mov       rdx,7FFB2DBD13D0
       7FFB2D79ADAD call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFB2D79ADB2 mov       rcx,rax
M02_L07:
       7FFB2D79ADB5 call      CORINFO_HELP_NEWSFAST
       7FFB2D79ADBA mov       r14,rax
       7FFB2D79ADBD mov       rcx,[r15+10]
       7FFB2D79ADC1 mov       r11,7FFB2D610580
       7FFB2D79ADCB call      qword ptr [r11]
       7FFB2D79ADCE mov       r13d,eax
       7FFB2D79ADD1 mov       rcx,r14
       7FFB2D79ADD4 mov       rdx,r15
       7FFB2D79ADD7 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__3(Int32, System.Threading.Tasks.ParallelLoopState, System.__Canon)
       7FFB2D79ADE1 call      qword ptr [7FFB2D754210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFB2D79ADE7 mov       rcx,[rbx+10]
       7FFB2D79ADEB mov       rdx,[rcx+28]
       7FFB2D79ADEF test      rdx,rdx
       7FFB2D79ADF2 je        short M02_L08
       7FFB2D79ADF4 jmp       short M02_L09
M02_L08:
       7FFB2D79ADF6 mov       rcx,rbx
       7FFB2D79ADF9 mov       rdx,7FFB2DBD2320
       7FFB2D79AE03 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFB2D79AE08 mov       rdx,rax
M02_L09:
       7FFB2D79AE0B mov       [rbp+30],rdi
       7FFB2D79AE0F xor       ecx,ecx
       7FFB2D79AE11 mov       [rbp+38],rcx
       7FFB2D79AE15 mov       [rbp+40],rcx
       7FFB2D79AE19 mov       [rbp+48],r14
       7FFB2D79AE1D mov       r14,[rbp+58]
       7FFB2D79AE21 mov       [rbp+50],r14
       7FFB2D79AE25 mov       r12,[rbp+60]
       7FFB2D79AE29 mov       [rbp+58],r12
       7FFB2D79AE2D mov       rcx,rsi
       7FFB2D79AE30 mov       r9d,r13d
       7FFB2D79AE33 xor       r8d,r8d
       7FFB2D79AE36 add       rsp,38
       7FFB2D79AE3A pop       rbx
       7FFB2D79AE3B pop       rsi
       7FFB2D79AE3C pop       rdi
       7FFB2D79AE3D pop       r12
       7FFB2D79AE3F pop       r13
       7FFB2D79AE41 pop       r14
       7FFB2D79AE43 pop       r15
       7FFB2D79AE45 pop       rbp
       7FFB2D79AE46 jmp       qword ptr [7FFB2DBC7138]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
M02_L10:
       7FFB2D79AE4C mov       rcx,[rbx+10]
       7FFB2D79AE50 mov       rcx,[rcx+20]
       7FFB2D79AE54 test      rcx,rcx
       7FFB2D79AE57 je        short M02_L11
       7FFB2D79AE59 jmp       short M02_L12
M02_L11:
       7FFB2D79AE5B mov       rcx,rbx
       7FFB2D79AE5E mov       rdx,7FFB2DBD13D0
       7FFB2D79AE68 call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFB2D79AE6D mov       rcx,rax
M02_L12:
       7FFB2D79AE70 call      CORINFO_HELP_NEWSFAST
       7FFB2D79AE75 mov       r13,rax
       7FFB2D79AE78 mov       rcx,[r15+10]
       7FFB2D79AE7C mov       r11,7FFB2D610578
       7FFB2D79AE86 call      qword ptr [r11]
       7FFB2D79AE89 mov       [rbp-44],eax
       7FFB2D79AE8C mov       rcx,r13
       7FFB2D79AE8F mov       rdx,r15
       7FFB2D79AE92 mov       r8,offset System.Threading.Tasks.Parallel+<>c__DisplayClass32_0`2[[System.Int32, System.Private.CoreLib],[System.__Canon, System.Private.CoreLib]].<ForEachWorker>b__4(Int32, System.Threading.Tasks.ParallelLoopState, System.__Canon)
       7FFB2D79AE9C call      qword ptr [7FFB2D754210]; System.MulticastDelegate.CtorClosed(System.Object, IntPtr)
       7FFB2D79AEA2 mov       rcx,[rbx+10]
       7FFB2D79AEA6 mov       rdx,[rcx+28]
       7FFB2D79AEAA test      rdx,rdx
       7FFB2D79AEAD je        short M02_L13
       7FFB2D79AEAF jmp       short M02_L14
M02_L13:
       7FFB2D79AEB1 mov       rcx,rbx
       7FFB2D79AEB4 mov       rdx,7FFB2DBD2320
       7FFB2D79AEBE call      CORINFO_HELP_RUNTIMEHANDLE_METHOD
       7FFB2D79AEC3 mov       rdx,rax
M02_L14:
       7FFB2D79AEC6 mov       [rbp+30],rdi
       7FFB2D79AECA xor       ecx,ecx
       7FFB2D79AECC mov       [rbp+38],rcx
       7FFB2D79AED0 mov       [rbp+40],rcx
       7FFB2D79AED4 mov       [rbp+48],r13
       7FFB2D79AED8 mov       r14,[rbp+58]
       7FFB2D79AEDC mov       [rbp+50],r14
       7FFB2D79AEE0 mov       r12,[rbp+60]
       7FFB2D79AEE4 mov       [rbp+58],r12
       7FFB2D79AEE8 mov       rcx,rsi
       7FFB2D79AEEB mov       r9d,[rbp-44]
       7FFB2D79AEEF xor       r8d,r8d
       7FFB2D79AEF2 add       rsp,38
       7FFB2D79AEF6 pop       rbx
       7FFB2D79AEF7 pop       rsi
       7FFB2D79AEF8 pop       rdi
       7FFB2D79AEF9 pop       r12
       7FFB2D79AEFB pop       r13
       7FFB2D79AEFD pop       r14
       7FFB2D79AEFF pop       r15
       7FFB2D79AF01 pop       rbp
       7FFB2D79AF02 jmp       qword ptr [7FFB2DBC7138]; System.Threading.Tasks.Parallel.ForWorker[[System.__Canon, System.Private.CoreLib],[System.Int32, System.Private.CoreLib]](Int32, Int32, System.Threading.Tasks.ParallelOptions, System.Action`1<Int32>, System.Action`2<Int32,System.Threading.Tasks.ParallelLoopState>, System.Func`4<Int32,System.Threading.Tasks.ParallelLoopState,System.__Canon,System.__Canon>, System.Func`1<System.__Canon>, System.Action`1<System.__Canon>)
       7FFB2D79AF08 add       rsp,38
       7FFB2D79AF0C pop       rbx
       7FFB2D79AF0D pop       rsi
       7FFB2D79AF0E pop       rdi
       7FFB2D79AF0F pop       r12
       7FFB2D79AF11 pop       r13
       7FFB2D79AF13 pop       r14
       7FFB2D79AF15 pop       r15
       7FFB2D79AF17 pop       rbp
       7FFB2D79AF18 ret
M02_L15:
       7FFB2D79AF19 mov       r11,7FFB2D610598
       7FFB2D79AF23 call      qword ptr [r11]
       7FFB2D79AF26 mov       ebx,eax
       7FFB2D79AF28 jmp       near ptr M02_L02
; Total bytes of code 1005
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         List.AsParallel().ForAll(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2D7ADAA0 push      rbx
       7FFB2D7ADAA1 sub       rsp,20
       7FFB2D7ADAA5 mov       rbx,rcx
       7FFB2D7ADAA8 mov       rcx,[rbx+8]
       7FFB2D7ADAAC call      qword ptr [7FFB2DBD6F40]; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFB2D7ADAB2 mov       rcx,rax
       7FFB2D7ADAB5 mov       rdx,[rbx+10]
       7FFB2D7ADAB9 call      qword ptr [7FFB2DBD74F8]; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFB2D7ADABF mov       eax,[rbx+1C]
       7FFB2D7ADAC2 add       rsp,20
       7FFB2D7ADAC6 pop       rbx
       7FFB2D7ADAC7 ret
; Total bytes of code 40
```
```assembly
; System.Linq.ParallelEnumerable.AsParallel[[System.Int32, System.Private.CoreLib]](System.Collections.Generic.IEnumerable`1<Int32>)
       7FFB2D7ADAE0 push      rdi
       7FFB2D7ADAE1 push      rsi
       7FFB2D7ADAE2 push      rbp
       7FFB2D7ADAE3 push      rbx
       7FFB2D7ADAE4 sub       rsp,58
       7FFB2D7ADAE8 xor       eax,eax
       7FFB2D7ADAEA mov       [rsp+28],rax
       7FFB2D7ADAEF vxorps    xmm4,xmm4,xmm4
       7FFB2D7ADAF3 vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFB2D7ADAF9 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFB2D7ADAFF mov       [rsp+50],rax
       7FFB2D7ADB04 mov       rbx,rcx
       7FFB2D7ADB07 test      rbx,rbx
       7FFB2D7ADB0A je        short M01_L00
       7FFB2D7ADB0C mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFB2D7ADB16 call      CORINFO_HELP_NEWSFAST
       7FFB2D7ADB1B mov       rbp,rax
       7FFB2D7ADB1E lea       rcx,[rsp+28]
       7FFB2D7ADB23 call      qword ptr [7FFB2DBD7348]; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFB2D7ADB29 lea       rdi,[rbp+8]
       7FFB2D7ADB2D lea       rsi,[rsp+28]
       7FFB2D7ADB32 call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2D7ADB37 call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2D7ADB3C mov       ecx,4
       7FFB2D7ADB41 rep movsq
       7FFB2D7ADB44 lea       rcx,[rbp+38]
       7FFB2D7ADB48 mov       rdx,rbx
       7FFB2D7ADB4B call      CORINFO_HELP_ASSIGN_REF
       7FFB2D7ADB50 mov       rax,rbp
       7FFB2D7ADB53 add       rsp,58
       7FFB2D7ADB57 pop       rbx
       7FFB2D7ADB58 pop       rbp
       7FFB2D7ADB59 pop       rsi
       7FFB2D7ADB5A pop       rdi
       7FFB2D7ADB5B ret
M01_L00:
       7FFB2D7ADB5C mov       ecx,6F1
       7FFB2D7ADB61 mov       rdx,7FFB2DBC4AF0
       7FFB2D7ADB6B call      CORINFO_HELP_STRCNS
       7FFB2D7ADB70 mov       rcx,rax
       7FFB2D7ADB73 call      qword ptr [7FFB2D886790]
       7FFB2D7ADB79 int       3
; Total bytes of code 154
```
```assembly
; System.Linq.ParallelEnumerable.ForAll[[System.Int32, System.Private.CoreLib]](System.Linq.ParallelQuery`1<Int32>, System.Action`1<Int32>)
       7FFB2D7ADC30 push      r15
       7FFB2D7ADC32 push      r14
       7FFB2D7ADC34 push      rdi
       7FFB2D7ADC35 push      rsi
       7FFB2D7ADC36 push      rbp
       7FFB2D7ADC37 push      rbx
       7FFB2D7ADC38 sub       rsp,58
       7FFB2D7ADC3C vzeroupper
       7FFB2D7ADC3F xor       eax,eax
       7FFB2D7ADC41 mov       [rsp+28],rax
       7FFB2D7ADC46 vxorps    xmm4,xmm4,xmm4
       7FFB2D7ADC4A vmovdqa   xmmword ptr [rsp+30],xmm4
       7FFB2D7ADC50 vmovdqa   xmmword ptr [rsp+40],xmm4
       7FFB2D7ADC56 mov       [rsp+50],rax
       7FFB2D7ADC5B mov       rsi,rcx
       7FFB2D7ADC5E mov       rbx,rdx
       7FFB2D7ADC61 test      rsi,rsi
       7FFB2D7ADC64 je        near ptr M02_L00
       7FFB2D7ADC6A test      rbx,rbx
       7FFB2D7ADC6D je        near ptr M02_L01
       7FFB2D7ADC73 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFB2D7ADC7D call      CORINFO_HELP_NEWSFAST
       7FFB2D7ADC82 mov       rbp,rax
       7FFB2D7ADC85 mov       rcx,rsi
       7FFB2D7ADC88 call      qword ptr [7FFB2DBDC150]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFB2D7ADC8E mov       r14,rax
       7FFB2D7ADC91 movzx     r15d,byte ptr [r14+38]
       7FFB2D7ADC96 vmovdqu   ymm0,ymmword ptr [r14+8]
       7FFB2D7ADC9C vmovdqu   ymmword ptr [rsp+28],ymm0
       7FFB2D7ADCA2 vmovdqu   xmm0,xmmword ptr [r14+28]
       7FFB2D7ADCA8 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFB2D7ADCAE mov       byte ptr [rbp+48],3
       7FFB2D7ADCB2 lea       rdi,[rbp+8]
       7FFB2D7ADCB6 lea       rsi,[rsp+28]
       7FFB2D7ADCBB call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2D7ADCC0 call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2D7ADCC5 mov       ecx,4
       7FFB2D7ADCCA rep movsq
       7FFB2D7ADCCD mov       [rbp+38],r15b
       7FFB2D7ADCD1 lea       rcx,[rbp+40]
       7FFB2D7ADCD5 mov       rdx,r14
       7FFB2D7ADCD8 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D7ADCDD lea       rcx,[rbp+50]
       7FFB2D7ADCE1 mov       rdx,rbx
       7FFB2D7ADCE4 call      CORINFO_HELP_ASSIGN_REF
       7FFB2D7ADCE9 mov       rcx,rbp
       7FFB2D7ADCEC add       rsp,58
       7FFB2D7ADCF0 pop       rbx
       7FFB2D7ADCF1 pop       rbp
       7FFB2D7ADCF2 pop       rsi
       7FFB2D7ADCF3 pop       rdi
       7FFB2D7ADCF4 pop       r14
       7FFB2D7ADCF6 pop       r15
       7FFB2D7ADCF8 jmp       qword ptr [7FFB2DBDC258]; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
M02_L00:
       7FFB2D7ADCFE mov       ecx,6F1
       7FFB2D7ADD03 mov       rdx,7FFB2DBC4AF0
       7FFB2D7ADD0D call      CORINFO_HELP_STRCNS
       7FFB2D7ADD12 mov       rcx,rax
       7FFB2D7ADD15 call      qword ptr [7FFB2D886790]
       7FFB2D7ADD1B int       3
M02_L01:
       7FFB2D7ADD1C mov       ecx,733
       7FFB2D7ADD21 mov       rdx,7FFB2DBC4AF0
       7FFB2D7ADD2B call      CORINFO_HELP_STRCNS
       7FFB2D7ADD30 mov       rcx,rax
       7FFB2D7ADD33 call      qword ptr [7FFB2D886790]
       7FFB2D7ADD39 int       3
; Total bytes of code 266
```

## .NET 8.0.7 (8.0.724.31311), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
;         var sum = 0;
;         ^^^^^^^^^^^^
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
;             sum += DoSomeThing(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2D799740 push      r14
       7FFB2D799742 push      rdi
       7FFB2D799743 push      rsi
       7FFB2D799744 push      rbp
       7FFB2D799745 push      rbx
       7FFB2D799746 sub       rsp,20
       7FFB2D79974A mov       rbx,rcx
       7FFB2D79974D xor       esi,esi
       7FFB2D79974F mov       rdx,[rbx+8]
       7FFB2D799753 test      rdx,rdx
       7FFB2D799756 je        short M00_L05
       7FFB2D799758 mov       rdi,[rdx+8]
       7FFB2D79975C mov       ebp,[rdx+10]
       7FFB2D79975F test      rdi,rdi
       7FFB2D799762 je        short M00_L03
       7FFB2D799764 cmp       [rdi+8],ebp
       7FFB2D799767 jb        short M00_L04
       7FFB2D799769 add       rdi,10
M00_L00:
       7FFB2D79976D xor       r14d,r14d
       7FFB2D799770 test      ebp,ebp
       7FFB2D799772 jle       short M00_L02
M00_L01:
       7FFB2D799774 mov       edx,r14d
       7FFB2D799777 mov       edx,[rdi+rdx*4]
       7FFB2D79977A mov       rcx,rbx
       7FFB2D79977D call      qword ptr [7FFB2DA0EE50]; Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFB2D799783 add       esi,eax
       7FFB2D799785 inc       r14d
       7FFB2D799788 cmp       r14d,ebp
       7FFB2D79978B jl        short M00_L01
M00_L02:
       7FFB2D79978D mov       eax,esi
       7FFB2D79978F add       rsp,20
       7FFB2D799793 pop       rbx
       7FFB2D799794 pop       rbp
       7FFB2D799795 pop       rsi
       7FFB2D799796 pop       rdi
       7FFB2D799797 pop       r14
       7FFB2D799799 ret
M00_L03:
       7FFB2D79979A test      ebp,ebp
       7FFB2D79979C jne       short M00_L04
       7FFB2D79979E xor       edi,edi
       7FFB2D7997A0 xor       ebp,ebp
       7FFB2D7997A2 jmp       short M00_L00
M00_L04:
       7FFB2D7997A4 call      qword ptr [7FFB2DA057E8]
       7FFB2D7997AA int       3
M00_L05:
       7FFB2D7997AB xor       edi,edi
       7FFB2D7997AD xor       ebp,ebp
       7FFB2D7997AF jmp       short M00_L00
; Total bytes of code 113
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFB2D7993A0 lea       eax,[rdx+rdx]
       7FFB2D7993A3 ret
; Total bytes of code 4
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For()
;         var sum = 0;
;         ^^^^^^^^^^^^
;         for (int i = 0; i < List.Count; i++)
;              ^^^^^^^^^
;             sum += DoSomeThing(List[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2C5151C0 push      rdi
       7FFB2C5151C1 push      rsi
       7FFB2C5151C2 push      rbx
       7FFB2C5151C3 sub       rsp,20
       7FFB2C5151C7 mov       rbx,rcx
       7FFB2C5151CA xor       esi,esi
       7FFB2C5151CC xor       edi,edi
       7FFB2C5151CE mov       rdx,[rbx+8]
       7FFB2C5151D2 cmp       dword ptr [rdx+10],0
       7FFB2C5151D6 jle       short M00_L01
M00_L00:
       7FFB2C5151D8 mov       rdx,[rbx+8]
       7FFB2C5151DC cmp       edi,[rdx+10]
       7FFB2C5151DF jae       short M00_L02
       7FFB2C5151E1 mov       rdx,[rdx+8]
       7FFB2C5151E5 cmp       edi,[rdx+8]
       7FFB2C5151E8 jae       short M00_L03
       7FFB2C5151EA mov       edx,[rdx+rdi*4+10]
       7FFB2C5151EE mov       rcx,rbx
       7FFB2C5151F1 call      qword ptr [7FFB2C8B5218]; Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFB2C5151F7 add       esi,eax
       7FFB2C5151F9 inc       edi
       7FFB2C5151FB mov       rax,[rbx+8]
       7FFB2C5151FF cmp       edi,[rax+10]
       7FFB2C515202 jl        short M00_L00
M00_L01:
       7FFB2C515204 mov       eax,esi
       7FFB2C515206 add       rsp,20
       7FFB2C51520A pop       rbx
       7FFB2C51520B pop       rsi
       7FFB2C51520C pop       rdi
       7FFB2C51520D ret
M00_L02:
       7FFB2C51520E call      qword ptr [7FFB2C8B5248]
       7FFB2C515214 int       3
M00_L03:
       7FFB2C515215 call      CORINFO_HELP_RNGCHKFAIL
       7FFB2C51521A int       3
; Total bytes of code 91
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFB2C5150A0 lea       eax,[rdx+rdx]
       7FFB2C5150A3 ret
; Total bytes of code 4
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Linq()
;         List.ForEach(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2C529F00 push      rbx
       7FFB2C529F01 sub       rsp,20
       7FFB2C529F05 mov       rbx,rcx
       7FFB2C529F08 mov       rcx,[rbx+8]
       7FFB2C529F0C mov       rdx,[rbx+10]
       7FFB2C529F10 cmp       [rcx],ecx
       7FFB2C529F12 call      qword ptr [7FFB2C904408]; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFB2C529F18 mov       eax,[rbx+1C]
       7FFB2C529F1B add       rsp,20
       7FFB2C529F1F pop       rbx
       7FFB2C529F20 ret
; Total bytes of code 33
```
```assembly
; System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib]].ForEach(System.Action`1<Int32>)
       7FFB2C529F40 push      r14
       7FFB2C529F42 push      rdi
       7FFB2C529F43 push      rsi
       7FFB2C529F44 push      rbp
       7FFB2C529F45 push      rbx
       7FFB2C529F46 sub       rsp,20
       7FFB2C529F4A mov       rbx,rcx
       7FFB2C529F4D mov       rsi,rdx
       7FFB2C529F50 test      rsi,rsi
       7FFB2C529F53 je        near ptr M01_L06
       7FFB2C529F59 mov       edi,[rbx+14]
       7FFB2C529F5C xor       ebp,ebp
       7FFB2C529F5E cmp       dword ptr [rbx+10],0
       7FFB2C529F62 jle       short M01_L01
       7FFB2C529F64 mov       r14,[rsi+18]
       7FFB2C529F68 mov       rdx,7FFB2C828CA8
       7FFB2C529F72 cmp       r14,rdx
       7FFB2C529F75 jne       short M01_L02
M01_L00:
       7FFB2C529F77 cmp       edi,[rbx+14]
       7FFB2C529F7A jne       short M01_L01
       7FFB2C529F7C mov       rdx,[rbx+8]
       7FFB2C529F80 cmp       ebp,[rdx+8]
       7FFB2C529F83 jae       short M01_L07
       7FFB2C529F85 mov       ecx,ebp
       7FFB2C529F87 mov       edx,[rdx+rcx*4+10]
       7FFB2C529F8B mov       rcx,[rsi+8]
       7FFB2C529F8F add       edx,edx
       7FFB2C529F91 add       [rcx+1C],edx
       7FFB2C529F94 inc       ebp
       7FFB2C529F96 cmp       ebp,[rbx+10]
       7FFB2C529F99 jl        short M01_L00
M01_L01:
       7FFB2C529F9B cmp       edi,[rbx+14]
       7FFB2C529F9E jne       short M01_L05
       7FFB2C529FA0 add       rsp,20
       7FFB2C529FA4 pop       rbx
       7FFB2C529FA5 pop       rbp
       7FFB2C529FA6 pop       rsi
       7FFB2C529FA7 pop       rdi
       7FFB2C529FA8 pop       r14
       7FFB2C529FAA ret
M01_L02:
       7FFB2C529FAB cmp       edi,[rbx+14]
       7FFB2C529FAE jne       short M01_L01
       7FFB2C529FB0 mov       rdx,[rbx+8]
       7FFB2C529FB4 cmp       ebp,[rdx+8]
       7FFB2C529FB7 jae       short M01_L07
       7FFB2C529FB9 mov       ecx,ebp
       7FFB2C529FBB mov       edx,[rdx+rcx*4+10]
       7FFB2C529FBF mov       rcx,7FFB2C828CA8
       7FFB2C529FC9 cmp       r14,rcx
       7FFB2C529FCC jne       short M01_L04
       7FFB2C529FCE mov       rcx,[rsi+8]
       7FFB2C529FD2 add       edx,edx
       7FFB2C529FD4 add       [rcx+1C],edx
M01_L03:
       7FFB2C529FD7 inc       ebp
       7FFB2C529FD9 cmp       ebp,[rbx+10]
       7FFB2C529FDC jl        short M01_L02
       7FFB2C529FDE jmp       short M01_L01
M01_L04:
       7FFB2C529FE0 mov       rcx,[rsi+8]
       7FFB2C529FE4 call      qword ptr [rsi+18]
       7FFB2C529FE7 jmp       short M01_L03
M01_L05:
       7FFB2C529FE9 call      qword ptr [7FFB2C6E7A98]
       7FFB2C529FEF int       3
M01_L06:
       7FFB2C529FF0 mov       ecx,1C
       7FFB2C529FF5 call      qword ptr [7FFB2C6E7B88]
       7FFB2C529FFB int       3
M01_L07:
       7FFB2C529FFC call      CORINFO_HELP_RNGCHKFAIL
       7FFB2C52A001 int       3
; Total bytes of code 194
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_Parallel()
;         Parallel.ForEach(List, _doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2C52B940 push      rbp
       7FFB2C52B941 push      r14
       7FFB2C52B943 push      rdi
       7FFB2C52B944 push      rsi
       7FFB2C52B945 push      rbx
       7FFB2C52B946 sub       rsp,80
       7FFB2C52B94D lea       rbp,[rsp+0A0]
       7FFB2C52B955 xor       eax,eax
       7FFB2C52B957 mov       [rbp-40],rax
       7FFB2C52B95B mov       rbx,rcx
       7FFB2C52B95E mov       rsi,[rbx+8]
       7FFB2C52B962 mov       rdi,[rbx+10]
       7FFB2C52B966 test      rsi,rsi
       7FFB2C52B969 je        near ptr M00_L03
       7FFB2C52B96F test      rdi,rdi
       7FFB2C52B972 je        near ptr M00_L04
       7FFB2C52B978 mov       rdx,28B14C01470
       7FFB2C52B982 mov       r14,[rdx]
       7FFB2C52B985 mov       rdx,[r14+18]
       7FFB2C52B989 mov       [rbp-40],rdx
       7FFB2C52B98D cmp       qword ptr [rbp-40],0
       7FFB2C52B992 jne       short M00_L02
M00_L00:
       7FFB2C52B994 mov       rdx,rsi
       7FFB2C52B997 mov       rcx,offset MT_System.Int32[]
       7FFB2C52B9A1 call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFB2C52B9A6 test      rax,rax
       7FFB2C52B9A9 jne       near ptr M00_L05
       7FFB2C52B9AF mov       [rsp+20],rdi
       7FFB2C52B9B4 xor       ecx,ecx
       7FFB2C52B9B6 mov       [rsp+28],rcx
       7FFB2C52B9BB mov       [rsp+30],rcx
       7FFB2C52B9C0 mov       [rsp+38],rcx
       7FFB2C52B9C5 mov       [rsp+40],rcx
       7FFB2C52B9CA mov       [rsp+48],rcx
       7FFB2C52B9CF mov       [rsp+50],rcx
       7FFB2C52B9D4 lea       rcx,[rbp-38]
       7FFB2C52B9D8 mov       r8,rsi
       7FFB2C52B9DB mov       r9,r14
       7FFB2C52B9DE mov       rdx,7FFB2C8F6B90
       7FFB2C52B9E8 call      qword ptr [7FFB2C9047F8]
M00_L01:
       7FFB2C52B9EE mov       eax,[rbx+1C]
       7FFB2C52B9F1 add       rsp,80
       7FFB2C52B9F8 pop       rbx
       7FFB2C52B9F9 pop       rsi
       7FFB2C52B9FA pop       rdi
       7FFB2C52B9FB pop       r14
       7FFB2C52B9FD pop       rbp
       7FFB2C52B9FE ret
M00_L02:
       7FFB2C52B9FF mov       rdx,[rbp-40]
       7FFB2C52BA03 cmp       dword ptr [rdx+20],0
       7FFB2C52BA07 je        short M00_L00
       7FFB2C52BA09 jmp       near ptr M00_L06
M00_L03:
       7FFB2C52BA0E mov       ecx,3C3
       7FFB2C52BA13 mov       rdx,7FFB2C8F2640
       7FFB2C52BA1D call      CORINFO_HELP_STRCNS
       7FFB2C52BA22 mov       rcx,rax
       7FFB2C52BA25 call      qword ptr [7FFB2C90D590]
       7FFB2C52BA2B int       3
M00_L04:
       7FFB2C52BA2C mov       ecx,38B
       7FFB2C52BA31 mov       rdx,7FFB2C8F2640
       7FFB2C52BA3B call      CORINFO_HELP_STRCNS
       7FFB2C52BA40 mov       rcx,rax
       7FFB2C52BA43 call      qword ptr [7FFB2C90D590]
       7FFB2C52BA49 int       3
M00_L05:
       7FFB2C52BA4A mov       [rsp+20],rdi
       7FFB2C52BA4F xor       ecx,ecx
       7FFB2C52BA51 mov       [rsp+28],rcx
       7FFB2C52BA56 mov       [rsp+30],rcx
       7FFB2C52BA5B mov       [rsp+38],rcx
       7FFB2C52BA60 mov       [rsp+40],rcx
       7FFB2C52BA65 mov       [rsp+48],rcx
       7FFB2C52BA6A mov       [rsp+50],rcx
       7FFB2C52BA6F lea       rcx,[rbp-38]
       7FFB2C52BA73 mov       r8,rax
       7FFB2C52BA76 mov       r9,r14
       7FFB2C52BA79 mov       rdx,7FFB2C9866F8
       7FFB2C52BA83 call      qword ptr [7FFB2C904840]
       7FFB2C52BA89 jmp       near ptr M00_L01
M00_L06:
       7FFB2C52BA8E lea       rcx,[rbp-40]
       7FFB2C52BA92 call      qword ptr [7FFB2C90D6C8]
       7FFB2C52BA98 int       3
; Total bytes of code 345
```
```assembly
; System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny(Void*, System.Object)
       7FFB2C523120 push      rsi
       7FFB2C523121 push      rbx
       7FFB2C523122 test      rdx,rdx
       7FFB2C523125 je        short M01_L00
       7FFB2C523127 mov       r8,[rdx]
       7FFB2C52312A cmp       r8,rcx
       7FFB2C52312D jne       short M01_L01
M01_L00:
       7FFB2C52312F mov       rax,rdx
       7FFB2C523132 pop       rbx
       7FFB2C523133 pop       rsi
       7FFB2C523134 ret
M01_L01:
       7FFB2C523135 mov       rax,28B14C00038
       7FFB2C52313F mov       rax,[rax]
       7FFB2C523142 add       rax,10
       7FFB2C523146 rorx      r10,r8,20
       7FFB2C52314C xor       r10,rcx
       7FFB2C52314F mov       r9,9E3779B97F4A7C15
       7FFB2C523159 imul      r10,r9
       7FFB2C52315D mov       r9d,[rax]
       7FFB2C523160 shrx      r10,r10,r9
       7FFB2C523165 xor       r9d,r9d
M01_L02:
       7FFB2C523168 lea       r11d,[r10+1]
       7FFB2C52316C movsxd    r11,r11d
       7FFB2C52316F lea       r11,[r11+r11*2]
       7FFB2C523173 lea       r11,[rax+r11*8]
       7FFB2C523177 mov       ebx,[r11]
       7FFB2C52317A mov       rsi,[r11+8]
       7FFB2C52317E and       ebx,0FFFFFFFE
       7FFB2C523181 cmp       rsi,r8
       7FFB2C523184 jne       short M01_L04
       7FFB2C523186 mov       rsi,rcx
       7FFB2C523189 xor       rsi,[r11+10]
       7FFB2C52318D cmp       rsi,1
       7FFB2C523191 ja        short M01_L04
       7FFB2C523193 cmp       ebx,[r11]
       7FFB2C523196 jne       short M01_L05
M01_L03:
       7FFB2C523198 cmp       esi,1
       7FFB2C52319B je        short M01_L00
       7FFB2C52319D test      esi,esi
       7FFB2C52319F jne       short M01_L06
       7FFB2C5231A1 xor       edx,edx
       7FFB2C5231A3 jmp       short M01_L00
M01_L04:
       7FFB2C5231A5 test      ebx,ebx
       7FFB2C5231A7 je        short M01_L05
       7FFB2C5231A9 inc       r9d
       7FFB2C5231AC add       r10d,r9d
       7FFB2C5231AF and       r10d,[rax+4]
       7FFB2C5231B3 cmp       r9d,8
       7FFB2C5231B7 jl        short M01_L02
M01_L05:
       7FFB2C5231B9 mov       esi,2
       7FFB2C5231BE jmp       short M01_L03
M01_L06:
       7FFB2C5231C0 pop       rbx
       7FFB2C5231C1 pop       rsi
       7FFB2C5231C2 jmp       near ptr System.Runtime.CompilerServices.CastHelpers.IsInstanceOfAny_NoCacheLookup(Void*, System.Object)
; Total bytes of code 167
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.ForEach_LinqParallel()
;         List.AsParallel().ForAll(_doSomeThing);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2C5317D0 push      r15
       7FFB2C5317D2 push      r14
       7FFB2C5317D4 push      rdi
       7FFB2C5317D5 push      rsi
       7FFB2C5317D6 push      rbp
       7FFB2C5317D7 push      rbx
       7FFB2C5317D8 sub       rsp,88
       7FFB2C5317DF xor       eax,eax
       7FFB2C5317E1 mov       [rsp+28],rax
       7FFB2C5317E6 vxorps    xmm4,xmm4,xmm4
       7FFB2C5317EA vmovdqu   ymmword ptr [rsp+30],ymm4
       7FFB2C5317F0 vmovdqu   ymmword ptr [rsp+50],ymm4
       7FFB2C5317F6 vmovdqa   xmmword ptr [rsp+70],xmm4
       7FFB2C5317FC mov       [rsp+80],rax
       7FFB2C531804 mov       rbx,rcx
       7FFB2C531807 mov       rbp,[rbx+8]
       7FFB2C53180B test      rbp,rbp
       7FFB2C53180E je        near ptr M00_L00
       7FFB2C531814 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C53181E call      CORINFO_HELP_NEWSFAST
       7FFB2C531823 mov       r14,rax
       7FFB2C531826 lea       rcx,[rsp+58]
       7FFB2C53182B call      qword ptr [7FFB2C904750]; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFB2C531831 lea       rdi,[r14+8]
       7FFB2C531835 lea       rsi,[rsp+58]
       7FFB2C53183A call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2C53183F call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2C531844 mov       ecx,4
       7FFB2C531849 rep movsq
       7FFB2C53184C lea       rcx,[r14+38]
       7FFB2C531850 mov       rdx,rbp
       7FFB2C531853 call      CORINFO_HELP_ASSIGN_REF
       7FFB2C531858 mov       rbp,[rbx+10]
       7FFB2C53185C test      rbp,rbp
       7FFB2C53185F je        near ptr M00_L01
       7FFB2C531865 mov       rcx,offset MT_System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C53186F call      CORINFO_HELP_NEWSFAST
       7FFB2C531874 mov       r15,rax
       7FFB2C531877 mov       rcx,r14
       7FFB2C53187A call      qword ptr [7FFB2C904AE0]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFB2C531880 mov       rdx,rax
       7FFB2C531883 movzx     r8d,byte ptr [rdx+38]
       7FFB2C531888 vmovdqu   ymm0,ymmword ptr [rdx+8]
       7FFB2C53188D vmovdqu   ymmword ptr [rsp+28],ymm0
       7FFB2C531893 vmovdqu   xmm0,xmmword ptr [rdx+28]
       7FFB2C531898 vmovdqu   xmmword ptr [rsp+48],xmm0
       7FFB2C53189E mov       byte ptr [r15+48],3
       7FFB2C5318A3 lea       rdi,[r15+8]
       7FFB2C5318A7 lea       rsi,[rsp+28]
       7FFB2C5318AC call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2C5318B1 call      CORINFO_HELP_ASSIGN_BYREF
       7FFB2C5318B6 mov       ecx,4
       7FFB2C5318BB rep movsq
       7FFB2C5318BE mov       [r15+38],r8b
       7FFB2C5318C2 lea       rcx,[r15+40]
       7FFB2C5318C6 call      CORINFO_HELP_ASSIGN_REF
       7FFB2C5318CB lea       rcx,[r15+50]
       7FFB2C5318CF mov       rdx,rbp
       7FFB2C5318D2 call      CORINFO_HELP_ASSIGN_REF
       7FFB2C5318D7 mov       rcx,r15
       7FFB2C5318DA call      qword ptr [7FFB2C904CD8]; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
       7FFB2C5318E0 mov       eax,[rbx+1C]
       7FFB2C5318E3 vzeroupper
       7FFB2C5318E6 add       rsp,88
       7FFB2C5318ED pop       rbx
       7FFB2C5318EE pop       rbp
       7FFB2C5318EF pop       rsi
       7FFB2C5318F0 pop       rdi
       7FFB2C5318F1 pop       r14
       7FFB2C5318F3 pop       r15
       7FFB2C5318F5 ret
M00_L00:
       7FFB2C5318F6 mov       ecx,6F1
       7FFB2C5318FB mov       rdx,7FFB2C8F2638
       7FFB2C531905 call      CORINFO_HELP_STRCNS
       7FFB2C53190A mov       rcx,rax
       7FFB2C53190D call      qword ptr [7FFB2C90DCC8]
       7FFB2C531913 int       3
M00_L01:
       7FFB2C531914 mov       ecx,733
       7FFB2C531919 mov       rdx,7FFB2C8F2638
       7FFB2C531923 call      CORINFO_HELP_STRCNS
       7FFB2C531928 mov       rcx,rax
       7FFB2C53192B call      qword ptr [7FFB2C90DCC8]
       7FFB2C531931 int       3
; Total bytes of code 354
```
```assembly
; System.Linq.Parallel.QuerySettings.get_Empty()
       7FFB2C52E3E0 push      rsi
       7FFB2C52E3E1 push      rbx
       7FFB2C52E3E2 sub       rsp,28
       7FFB2C52E3E6 mov       rbx,rcx
       7FFB2C52E3E9 mov       rcx,offset MT_System.Linq.Parallel.CancellationState
       7FFB2C52E3F3 call      CORINFO_HELP_NEWSFAST
       7FFB2C52E3F8 mov       rsi,rax
       7FFB2C52E3FB xor       ecx,ecx
       7FFB2C52E3FD mov       [rsi+20],rcx
       7FFB2C52E401 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFB2C52E40B call      CORINFO_HELP_NEWSFAST
       7FFB2C52E410 mov       byte ptr [rax+8],0
       7FFB2C52E414 lea       rcx,[rsi+18]
       7FFB2C52E418 mov       rdx,rax
       7FFB2C52E41B call      CORINFO_HELP_ASSIGN_REF
       7FFB2C52E420 xor       ecx,ecx
       7FFB2C52E422 mov       [rbx],rcx
       7FFB2C52E425 lea       rcx,[rbx+8]
       7FFB2C52E429 mov       rdx,rsi
       7FFB2C52E42C call      CORINFO_HELP_CHECKED_ASSIGN_REF
       7FFB2C52E431 mov       dword ptr [rbx+10],0FFFFFFFF
       7FFB2C52E438 mov       byte ptr [rbx+14],0
       7FFB2C52E43C xor       eax,eax
       7FFB2C52E43E mov       [rbx+18],eax
       7FFB2C52E441 mov       byte ptr [rbx+1C],0
       7FFB2C52E445 mov       [rbx+20],eax
       7FFB2C52E448 mov       byte ptr [rbx+24],0
       7FFB2C52E44C mov       [rbx+28],eax
       7FFB2C52E44F mov       rax,rbx
       7FFB2C52E452 add       rsp,28
       7FFB2C52E456 pop       rbx
       7FFB2C52E457 pop       rsi
       7FFB2C52E458 ret
; Total bytes of code 121
```
```assembly
; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].AsQueryOperator(System.Collections.Generic.IEnumerable`1<Int32>)
       7FFB2C531BB0 push      rdi
       7FFB2C531BB1 push      rsi
       7FFB2C531BB2 push      rbp
       7FFB2C531BB3 push      rbx
       7FFB2C531BB4 sub       rsp,28
       7FFB2C531BB8 mov       rbx,rcx
       7FFB2C531BBB mov       rax,rbx
       7FFB2C531BBE test      rax,rax
       7FFB2C531BC1 je        short M02_L00
       7FFB2C531BC3 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531BCD cmp       [rax],rcx
       7FFB2C531BD0 jne       near ptr M02_L04
       7FFB2C531BD6 xor       eax,eax
M02_L00:
       7FFB2C531BD8 test      rax,rax
       7FFB2C531BDB jne       near ptr M02_L03
       7FFB2C531BE1 mov       rsi,rbx
       7FFB2C531BE4 test      rsi,rsi
       7FFB2C531BE7 je        short M02_L01
       7FFB2C531BE9 mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531BF3 cmp       [rsi],rcx
       7FFB2C531BF6 jne       near ptr M02_L05
       7FFB2C531BFC xor       esi,esi
M02_L01:
       7FFB2C531BFE test      rsi,rsi
       7FFB2C531C01 jne       near ptr M02_L06
       7FFB2C531C07 mov       rcx,offset MT_System.Linq.Parallel.ScanQueryOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531C11 call      CORINFO_HELP_NEWSFAST
       7FFB2C531C16 mov       rsi,rax
       7FFB2C531C19 mov       rcx,offset MT_System.Linq.Parallel.CancellationState
       7FFB2C531C23 call      CORINFO_HELP_NEWSFAST
       7FFB2C531C28 mov       rdi,rax
       7FFB2C531C2B xor       ecx,ecx
       7FFB2C531C2D mov       [rdi+20],rcx
       7FFB2C531C31 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFB2C531C3B call      CORINFO_HELP_NEWSFAST
       7FFB2C531C40 mov       byte ptr [rax+8],0
       7FFB2C531C44 lea       rcx,[rdi+18]
       7FFB2C531C48 mov       rdx,rax
       7FFB2C531C4B call      CORINFO_HELP_ASSIGN_REF
       7FFB2C531C50 lea       rbp,[rsi+8]
       7FFB2C531C54 xor       ecx,ecx
       7FFB2C531C56 mov       [rbp],rcx
       7FFB2C531C5A lea       rcx,[rbp+8]
       7FFB2C531C5E mov       rdx,rdi
       7FFB2C531C61 call      CORINFO_HELP_ASSIGN_REF
       7FFB2C531C66 mov       dword ptr [rbp+10],0FFFFFFFF
       7FFB2C531C6D mov       byte ptr [rbp+14],0
       7FFB2C531C71 xor       ecx,ecx
       7FFB2C531C73 mov       [rbp+18],ecx
       7FFB2C531C76 mov       byte ptr [rbp+1C],0
       7FFB2C531C7A mov       [rbp+20],ecx
       7FFB2C531C7D mov       byte ptr [rbp+24],0
       7FFB2C531C81 mov       [rbp+28],ecx
       7FFB2C531C84 mov       byte ptr [rsi+38],0
       7FFB2C531C88 test      rbx,rbx
       7FFB2C531C8B je        short M02_L02
       7FFB2C531C8D mov       rcx,offset MT_System.Linq.Parallel.ParallelEnumerableWrapper`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531C97 cmp       [rbx],rcx
       7FFB2C531C9A jne       short M02_L02
       7FFB2C531C9C mov       rbx,[rbx+38]
M02_L02:
       7FFB2C531CA0 lea       rcx,[rsi+40]
       7FFB2C531CA4 mov       rdx,rbx
       7FFB2C531CA7 call      CORINFO_HELP_ASSIGN_REF
       7FFB2C531CAC mov       rax,rsi
M02_L03:
       7FFB2C531CAF add       rsp,28
       7FFB2C531CB3 pop       rbx
       7FFB2C531CB4 pop       rbp
       7FFB2C531CB5 pop       rsi
       7FFB2C531CB6 pop       rdi
       7FFB2C531CB7 ret
M02_L04:
       7FFB2C531CB8 mov       rdx,rbx
       7FFB2C531CBB mov       rcx,offset MT_System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531CC5 call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfClass(Void*, System.Object)
       7FFB2C531CCA jmp       near ptr M02_L00
M02_L05:
       7FFB2C531CCF mov       rdx,rbx
       7FFB2C531CD2 mov       rcx,offset MT_System.Linq.OrderedParallelQuery`1[[System.Int32, System.Private.CoreLib]]
       7FFB2C531CDC call      System.Runtime.CompilerServices.CastHelpers.IsInstanceOfClass(Void*, System.Object)
       7FFB2C531CE1 mov       rsi,rax
       7FFB2C531CE4 jmp       near ptr M02_L01
M02_L06:
       7FFB2C531CE9 mov       rax,[rsi+38]
       7FFB2C531CED jmp       short M02_L03
; Total bytes of code 319
```
```assembly
; System.Linq.Parallel.ForAllOperator`1[[System.Int32, System.Private.CoreLib]].RunSynchronously()
       7FFB2C531D10 push      r15
       7FFB2C531D12 push      r14
       7FFB2C531D14 push      rdi
       7FFB2C531D15 push      rsi
       7FFB2C531D16 push      rbp
       7FFB2C531D17 push      rbx
       7FFB2C531D18 sub       rsp,0C8
       7FFB2C531D1F vxorps    xmm4,xmm4,xmm4
       7FFB2C531D23 vmovdqu   ymmword ptr [rsp+30],ymm4
       7FFB2C531D29 vmovdqu   ymmword ptr [rsp+50],ymm4
       7FFB2C531D2F vmovdqu   ymmword ptr [rsp+70],ymm4
       7FFB2C531D35 vmovdqu   ymmword ptr [rsp+90],ymm4
       7FFB2C531D3E vmovdqa   xmmword ptr [rsp+0B0],xmm4
       7FFB2C531D47 xor       eax,eax
       7FFB2C531D49 mov       [rsp+0C0],rax
       7FFB2C531D51 mov       rbx,rcx
       7FFB2C531D54 mov       rcx,offset MT_System.Linq.Parallel.Shared`1[[System.Boolean, System.Private.CoreLib]]
       7FFB2C531D5E call      CORINFO_HELP_NEWSFAST
       7FFB2C531D63 mov       rsi,rax
       7FFB2C531D66 mov       byte ptr [rsi+8],0
       7FFB2C531D6A mov       rcx,offset MT_System.Threading.CancellationTokenSource
       7FFB2C531D74 call      CORINFO_HELP_NEWSFAST
       7FFB2C531D79 mov       r8,rax
       7FFB2C531D7C vmovdqu   ymm0,ymmword ptr [rbx+8]
       7FFB2C531D81 vmovdqu   ymmword ptr [rsp+68],ymm0
       7FFB2C531D87 vmovdqu   xmm0,xmmword ptr [rbx+28]
       7FFB2C531D8C vmovdqu   xmmword ptr [rsp+88],xmm0
       7FFB2C531D95 lea       rcx,[rsp+68]
       7FFB2C531D9A lea       rdx,[rsp+68]
       7FFB2C531D9F mov       r9,rsi
       7FFB2C531DA2 call      qword ptr [7FFB2C904D08]; System.Linq.Parallel.QuerySettings.WithPerExecutionSettings(System.Threading.CancellationTokenSource, System.Linq.Parallel.Shared`1<Boolean>)
       7FFB2C531DA8 lea       rcx,[rsp+68]
       7FFB2C531DAD lea       rdx,[rsp+98]
       7FFB2C531DB5 call      qword ptr [7FFB2C904FA8]; System.Linq.Parallel.QuerySettings.WithDefaults()
       7FFB2C531DBB mov       rcx,1E463C01480
       7FFB2C531DC5 mov       rsi,[rcx]
       7FFB2C531DC8 mov       rcx,rsi
       7FFB2C531DCB mov       edi,[rsp+0A8]
       7FFB2C531DD2 mov       edx,edi
       7FFB2C531DD4 call      qword ptr [7FFB2C904FD8]; System.Linq.Parallel.PlinqEtwProvider.ParallelQueryBegin(Int32)
       7FFB2C531DDA mov       byte ptr [rsp+60],1
       7FFB2C531DDF mov       dword ptr [rsp+64],3
       7FFB2C531DE7 vmovdqu   ymm0,ymmword ptr [rsp+98]
       7FFB2C531DF0 vmovdqu   ymmword ptr [rsp+30],ymm0
       7FFB2C531DF6 vmovdqu   xmm0,xmmword ptr [rsp+0B8]
       7FFB2C531DFF vmovdqu   xmmword ptr [rsp+50],xmm0
       7FFB2C531E05 mov       rdx,[rsp+60]
       7FFB2C531E0A lea       rcx,[rsp+30]
       7FFB2C531E0F mov       [rsp+20],rcx
       7FFB2C531E14 mov       rcx,rbx
       7FFB2C531E17 mov       r8d,1
       7FFB2C531E1D mov       r9d,1
       7FFB2C531E23 call      qword ptr [7FFB2C905008]; System.Linq.Parallel.QueryOperator`1[[System.Int32, System.Private.CoreLib]].GetOpenedEnumerator(System.Nullable`1<System.Linq.ParallelMergeOptions>, Boolean, Boolean, System.Linq.Parallel.QuerySettings)
       7FFB2C531E29 mov       rcx,[rsp+0A0]
       7FFB2C531E31 mov       rbx,[rcx+10]
       7FFB2C531E35 mov       rcx,offset MT_System.Threading.CancellationTokenSource+Linked1CancellationTokenSource
       7FFB2C531E3F cmp       [rbx],rcx
       7FFB2C531E42 jne       near ptr M03_L03
       7FFB2C531E48 cmp       byte ptr [rbx+24],0
       7FFB2C531E4C jne       short M03_L01
       7FFB2C531E4E lea       rbp,[rbx+28]
       7FFB2C531E52 mov       r14,[rbp]
       7FFB2C531E56 test      r14,r14
       7FFB2C531E59 jne       short M03_L02
M03_L00:
       7FFB2C531E5B mov       rcx,rbx
       7FFB2C531E5E mov       edx,1
       7FFB2C531E63 call      qword ptr [7FFB2C8FAA28]; System.Threading.CancellationTokenSource.Dispose(Boolean)
M03_L01:
       7FFB2C531E69 mov       rcx,rbx
       7FFB2C531E6C call      System.GC._SuppressFinalize(System.Object)
       7FFB2C531E71 mov       rcx,rsi
       7FFB2C531E74 mov       edx,edi
       7FFB2C531E76 call      qword ptr [7FFB2C907618]; System.Linq.Parallel.PlinqEtwProvider.ParallelQueryEnd(Int32)
       7FFB2C531E7C nop
       7FFB2C531E7D vzeroupper
       7FFB2C531E80 add       rsp,0C8
       7FFB2C531E87 pop       rbx
       7FFB2C531E88 pop       rbp
       7FFB2C531E89 pop       rsi
       7FFB2C531E8A pop       rdi
       7FFB2C531E8B pop       r14
       7FFB2C531E8D pop       r15
       7FFB2C531E8F ret
M03_L02:
       7FFB2C531E90 mov       rcx,[r14+8]
       7FFB2C531E94 mov       rdx,[rbp+8]
       7FFB2C531E98 mov       r8,r14
       7FFB2C531E9B cmp       [rcx],ecx
       7FFB2C531E9D call      qword ptr [7FFB2C907600]; System.Threading.CancellationTokenSource+Registrations.Unregister(Int64, CallbackNode)
       7FFB2C531EA3 test      eax,eax
       7FFB2C531EA5 jne       short M03_L00
       7FFB2C531EA7 mov       rbp,[rbp+8]
       7FFB2C531EAB mov       rax,[r14+8]
       7FFB2C531EAF mov       rax,[rax+8]
       7FFB2C531EB3 cmp       dword ptr [rax+20],0
       7FFB2C531EB7 je        short M03_L00
       7FFB2C531EB9 cmp       dword ptr [rax+20],2
       7FFB2C531EBD je        short M03_L00
       7FFB2C531EBF mov       rax,[r14+8]
       7FFB2C531EC3 mov       r15d,[rax+30]
       7FFB2C531EC7 call      CORINFO_HELP_GETCURRENTMANAGEDTHREADID
       7FFB2C531ECC cmp       r15d,eax
       7FFB2C531ECF je        short M03_L00
       7FFB2C531ED1 mov       rcx,[r14+8]
       7FFB2C531ED5 mov       rdx,rbp
       7FFB2C531ED8 cmp       [rcx],ecx
       7FFB2C531EDA call      qword ptr [7FFB2C90E6A0]
       7FFB2C531EE0 jmp       near ptr M03_L00
M03_L03:
       7FFB2C531EE5 mov       rcx,rbx
       7FFB2C531EE8 mov       edx,1
       7FFB2C531EED mov       rax,[rbx]
       7FFB2C531EF0 mov       rax,[rax+40]
       7FFB2C531EF4 call      qword ptr [rax+28]
       7FFB2C531EF7 jmp       near ptr M03_L01
; Total bytes of code 492
```

## .NET 9.0.0 (9.0.24.43107), X64 RyuJIT AVX2
```assembly
; Benchmark.BetterBenchmark.For_Span()
;         var sum = 0;
;         ^^^^^^^^^^^^
;         var span = CollectionsMarshal.AsSpan(List);
;         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         for (int i = 0; i < span.Length; i++)
;              ^^^^^^^^^
;             sum += DoSomeThing(span[i]);
;             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
;         return sum;
;         ^^^^^^^^^^^
       7FFB2C52A240 push      r14
       7FFB2C52A242 push      rdi
       7FFB2C52A243 push      rsi
       7FFB2C52A244 push      rbp
       7FFB2C52A245 push      rbx
       7FFB2C52A246 sub       rsp,20
       7FFB2C52A24A mov       rbx,rcx
       7FFB2C52A24D xor       esi,esi
       7FFB2C52A24F mov       rdx,[rbx+8]
       7FFB2C52A253 xor       edi,edi
       7FFB2C52A255 xor       ebp,ebp
       7FFB2C52A257 test      rdx,rdx
       7FFB2C52A25A je        short M00_L00
       7FFB2C52A25C mov       ebp,[rdx+10]
       7FFB2C52A25F mov       rdi,[rdx+8]
       7FFB2C52A263 cmp       [rdi+8],ebp
       7FFB2C52A266 jb        short M00_L03
       7FFB2C52A268 add       rdi,10
M00_L00:
       7FFB2C52A26C test      ebp,ebp
       7FFB2C52A26E jle       short M00_L02
       7FFB2C52A270 xor       r14d,r14d
M00_L01:
       7FFB2C52A273 mov       edx,[rdi+r14]
       7FFB2C52A277 mov       rcx,rbx
       7FFB2C52A27A call      qword ptr [7FFB2C904408]; Benchmark.BetterBenchmark.DoSomeThing(Int32)
       7FFB2C52A280 add       esi,eax
       7FFB2C52A282 add       r14,4
       7FFB2C52A286 dec       ebp
       7FFB2C52A288 jne       short M00_L01
M00_L02:
       7FFB2C52A28A mov       eax,esi
       7FFB2C52A28C add       rsp,20
       7FFB2C52A290 pop       rbx
       7FFB2C52A291 pop       rbp
       7FFB2C52A292 pop       rsi
       7FFB2C52A293 pop       rdi
       7FFB2C52A294 pop       r14
       7FFB2C52A296 ret
M00_L03:
       7FFB2C52A297 call      qword ptr [7FFB2C6E7390]
       7FFB2C52A29D int       3
; Total bytes of code 94
```
```assembly
; Benchmark.BetterBenchmark.DoSomeThing(Int32)
;     private int DoSomeThing(int i) => i + i;
;                                       ^^^^^
       7FFB2C529EC0 lea       eax,[rdx+rdx]
       7FFB2C529EC3 ret
; Total bytes of code 4
```

