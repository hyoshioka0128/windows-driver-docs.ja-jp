---
title: 注釈付き x64 逆アセンブリ
description: 注釈付き x64 逆アセンブリ
ms.assetid: 67930062-8a3a-460f-ae56-248d2a8e131e
keywords:
- x64 プロセッサ、注釈付き逆アセンブリ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62993cca9e37a60ae1a6b674e15bc219f10404c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355391"
---
# <a name="annotated-x64-disassembly"></a>注釈付き x64 逆アセンブリ


## <span id="ddk_annotated_x64_disassembly_dbg"></span><span id="DDK_ANNOTATED_X64_DISASSEMBLY_DBG"></span>


次の非常に単純な関数は、x64 呼び出し規則を示しています。

```cpp
int Simple(int i, int j)
{
    return i*5 + j + 3;
}
```

これは、このようなコードにコンパイルされます。

```dbgcmd
01001080 lea     eax,[rdx+rcx*4]        ; eax = rdx+rcx*4
01001083 lea     eax,[rcx+rax+0x3]      ; eax = rcx+rax+3
01001087 ret
```

*は*と*j*パラメーターは、 **ecx**と**edx**それぞれ登録します。 2 つのパラメーターがあるので、ルーチンを使用しません、スタックに。

生成された特定のコードでは、うちの 1 つは、x64 に固有の 3 つのテクニックを悪用します。

1.  **元に戻せる**一連の単純な算術演算を 1 回の操作を実行する操作を使用できます。 最初の命令ストア*j + は*\*で 4 **eax**、2 番目の命令を追加および*は*を合計の結果に +3 *j* +*は*\*5 + 3。

2.  加算や乗算など、多くの操作を余分な精度の実行し、適切な有効桁数に切り捨てられます。 このインスタンスでは、コードは、64 ビット加算や乗算を使用します。 32 ビットの結果は安全に切り詰められますことができます。

3.  X64 で 32 ビット レジスタに自動的に出力する操作を行うゼロ拡張結果。 出力するこの例では、 **eax**を 32 ビットの結果の切り捨ての効果があります。

戻り値が渡された、 **rax**を登録します。 この場合、結果は既に、 **rax**登録するため、関数を返します。

一般的な x64 を示すためにより複雑な関数を検討してください次に [逆アセンブル]。

```cpp
HRESULT Meaningless(IDispatch *pdisp, DISPID dispid, BOOL fUnique, LPCWSTR pszExe)
{
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
    if (SUCCEEDED(hr)) {
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);
        if (SUCCEEDED(hr)) {
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {
                VARIANTARG rgvarg[2] = { 0 };
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {
                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }
        }
        pqa->Release();
    }
    return hr;
}
```

行でこの関数と同等の組み立てラインを移動します。

入力すると、関数のパラメーターは、次のように格納されます。

-   **rcx** = *pdisp*します。

-   **rdx** = *dispid*します。

-   **r8** = *fUnique*します。

-   **r9** = *pszExe*します。

最初の 4 つのパラメーターがレジスタに渡されることを思い出してください。 この関数は 4 つだけのレジスタがあるので、[なし] はスタックに渡されます。

アセンブリに次のように始めます。

```dbgcmd
Meaningless:
010010e0 push    rbx                    ; save
010010e1 push    rsi                    ; save
010010e2 push    rdi                    ; save
010010e3 push    r12d                   ; save
010010e5 push    r13d                   ; save
010010e7 push    r14d                   ; save
010010e9 push    r15d                   ; save
010010eb sub     rsp,0x2c0              ; reserve stack
010010f2 mov     rbx,r9                 ; rbx = pszExe
010010f5 mov     r12d,r8d               ; r12 = fUnique (zero-extend)
010010f8 mov     r13d,edx               ; r13 = dispid  (zero-extend)
010010fb mov     rsi,rcx                ; rsi = pdisp
```

関数は、不揮発性レジスタを保存し、ローカル変数のスタック領域を予約し、開始します。 パラメーターは、不揮発性レジスタにし、保存します。 なお、中間の 2 つのコピー先**mov** 64 ビットに暗黙的にゼロ拡張されるため、手順については、32 ビット レジスタ。

```dbgcmd
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
```

最初のパラメーター **AssocCreate**は値によって渡される 128 ビットの CLSID。 64 ビット レジスタに収まらないこれ以降は、スタックに CLSID がコピーされ、スタックの場所へのポインターが代わりに渡されます。

```dbgcmd
010010fe movdqu  xmm0,oword ptr [CLSID_QueryAssociations (01001060)]
01001106 movdqu  oword ptr [rsp+0x60],xmm0  ; temp buffer for first parameter
0100110c lea     r8,[rsp+0x58]          ; arg3 = &pqa
01001111 lea rdx,[IID_IQueryAssociations (01001070)] ; arg2 = &IID_IQueryAssociations
01001118 lea     rcx,[rsp+0x60]         ; arg1 = &temporary
0100111d call qword ptr [_imp_AssocCreate (01001028)] ; call
```

**Movdqu**命令との間に 128 ビット値を転送 **xmm * * * n*を登録します。 このインスタンスでアセンブリ コードは、それをスタックに CLSID をコピーするのに使用します。 CLSID へのポインターが渡された**r8**します。 その他の 2 つの引数が渡された**rcx**と**rdx**します。

```dbgcmd
    if (SUCCEEDED(hr)) {

01001123 test    eax,eax
01001125 jl      ReturnEAX (01001281)
```

コードは、戻り値が成功したかどうかを確認します。

```dbgcmd
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);

0100112b mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001130 mov     rax,[rcx]              ; rax = pqa.vtbl
01001133 xor     r14d,r14d              ; r14 = 0
01001136 mov     [rsp+0x20],r14         ; arg5 = 0
0100113b xor     r9d,r9d                ; arg4 = 0
0100113e mov     r8,rbx                 ; arg3 = pszExe
01001141 mov     r15d,0x2               ; r15 = 2 (for later)
01001147 mov     edx,r15d               ; arg2 = 2 (ASSOCF_INIT_BY_EXENAME)
0100114a call    qword ptr [rax+0x18]   ; call Init method
```

これは、C++、vtable を使用して間接的な関数呼び出しです。 **この**ポインターが渡された**rcx**最初のパラメーターとして。 最初の 3 つのパラメーターは、最後のパラメーターがスタックに渡されるときに、レジスタに渡されます。 関数は、5 番目のパラメーターから開始するために、レジスタに渡されるパラメーターを 16 バイトの予約**rsp**+ 0x20。

```dbgcmd
        if (SUCCEEDED(hr)) {

0100114d mov     ebx,eax                ; ebx = hr
0100114f test    ebx,ebx                ; FAILED?
01001151 jl      ReleasePQA (01001274)  ; jump if so
```

アセンブリ言語のコードで結果を保存します**ebx**、およびそれが成功コードであるかどうかをチェックします。

```dbgcmd
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {

01001157 mov     dword ptr [rsp+0x50],0x104 ; cchName = MAX_PATH
0100115f mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001164 mov     rax,[rcx]              ; rax = pqa.vtbl
01001167 lea     rdx,[rsp+0x50]         ; rdx = &cchName
0100116c mov     [rsp+0x28],rdx         ; arg6 = cchName
01001171 lea     rdx,[rsp+0xb0]         ; rdx = &wszName[0]
01001179 mov     [rsp+0x20],rdx         ; arg5 = &wszName[0]
0100117e xor     r9d,r9d                ; arg4 = 0
01001181 mov     r8d,0x4                ; arg3 = 4 (ASSOCSTR_FRIENDLYNAME)
01001187 xor     edx,edx                ; arg2 = 0
01001189 call    qword ptr [rax+0x20]   ; call GetString method
0100118c mov     ebx,eax                ; ebx = hr
0100118e test    ebx,ebx                ; FAILED?
01001190 jl      ReleasePQA (01001274)  ; jump if so
```

もう一度、関数を呼び出すとし、テスト成功の戻り値パラメーターを設定します。

```dbgcmd
                VARIANTARG rgvarg[2] = { 0 };

01001196 lea     rdi,[rsp+0x82]         ; rdi = &rgvarg
0100119e xor     eax,eax                ; rax = 0
010011a0 mov     ecx,0x2e               ; rcx = sizeof(rgvarg)
010011a5 rep     stosb                  ; Zero it out
```

X64 でのバッファー領域の解放の慣用メソッドでは、x86 の場合と同じです。

```dbgcmd
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {

010011a7 mov     word ptr [rsp+0x80],0x8 ; V_VT(&rgvarg[0]) = VT_BSTR
010011b1 lea     rcx,[rsp+0xb0]         ; arg1 = &wszName[0]
010011b9 call    qword ptr [_imp_SysAllocString (01001010)] ; call
010011bf mov     [rsp+0x88],rax         ; V_BSTR(&rgvarg[0]) = result
010011c7 test    rax,rax                ; anything allocated?
010011ca je      OutOfMemory (0100126f) ; jump if failed

                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);

010011d0 lea     rax,[lCounter (01002000)]
010011d7 mov     ecx,0x1
010011dc lock    xadd [rax],ecx             ; interlocked exchange and add
010011e0 add     ecx,0x1
```

**InterlockedIncrement**マシン語コードに直接コンパイルされます。 **ロック xadd**命令は、アトミックの交換を実行し、追加します。 最終的な結果が格納されている**ecx**します。

```dbgcmd
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;

010011e3 mov     word ptr [rsp+0x98],0x3    ; V_VT(&rgvarg[1]) = VT_I4;
010011ed mov     eax,r14d                   ; rax = 0 (r14d is still zero)
010011f0 test    r12d,r12d                  ; fUnique set?
010011f3 cmovne  eax,ecx                    ; if so, then set rax=lCounter
010011f6 mov     [rsp+0xa0],eax             ; V_I4(&rgvarg[1]) = ...
```

X64 がサポートされているので、 **cmov** 、命令、**でしょうか。:** ジャンプを使用せず、コンストラクトをコンパイルできます。

```dbgcmd
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;

010011fd lea     rax,[rsp+0x80]             ; rax = &rgvarg[0]
01001205 mov     [rsp+0x60],rax             ; dp.rgvarg = rgvarg
0100120a mov     [rsp+0x70],r15d            ; dp.cArgs = 2 (r15 is still 2)
0100120f mov     [rsp+0x68],r14             ; dp.rgdispidNamedArgs = NULL
01001214 mov     [rsp+0x74],r14d            ; dp.cNamedArgs = 0
```

このコードでは、DISPPARAMS のメンバーの残りの部分を初期化します。 コンパイラが CLSID で使用していたスタック上の領域を再利用することに注意してください。

```dbgcmd
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);

01001219 mov     rax,[rsi]                  ; rax = pdisp.vtbl
0100121c mov     [rsp+0x40],r14             ; arg9 = 0
01001221 mov     [rsp+0x38],r14             ; arg8 = 0
01001226 mov     [rsp+0x30],r14             ; arg7 = 0
0100122b lea     rcx,[rsp+0x60]             ; rcx = &dp
01001230 mov     [rsp+0x28],rcx             ; arg6 = &dp
01001235 mov     word ptr [rsp+0x20],0x1    ; arg5 = 1 (DISPATCH_METHOD)
0100123c xor     r9d,r9d                    ; arg4 = 0
0100123f lea     r8,[GUID_NULL (01001080)]  ; arg3 = &IID_NULL
01001246 mov     edx,r13d                   ; arg2 = dispid
01001249 mov     rcx,rsi                    ; arg1 = pdisp
0100124c call    qword ptr [rax+0x30]       ; call Invoke method
0100124f mov     ebx,eax                    ; hr = result
```

パラメーターと呼び出しを設定し、 **Invoke**メソッド。

```dbgcmd
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);

01001251 lea     rcx,[rsp+0x80]             ; arg1 = &rgvarg[0]
01001259 call    qword ptr [_imp_VariantClear (01001018)]
0100125f lea     rcx,[rsp+0x98]             ; arg1 = &rgvarg[1]
01001267 call    qword ptr [_imp_VariantClear (01001018)]
0100126d jmp     ReleasePQA (01001274)
```

コードが完了し、条件付きの現在のブランチとスキップする、**他**分岐します。

```dbgcmd
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }

OutOfMemory:
0100126f mov     ebx,0x8007000e             ; hr = E_OUTOFMEMORY
        pqa->Release();
ReleasePQA:
01001274 mov     rcx,[rsp+0x58]             ; arg1 = pqa
01001279 mov     rax,[rcx]                  ; rax = pqa.vtbl
0100127c call    qword ptr [rax+0x10]       ; release
```

**他**分岐します。

```dbgcmd
    return hr;
}

0100127f mov     eax,ebx                    ; rax = hr (for return value)
ReturnEAX:
01001281 add     rsp,0x2c0                  ; clean up the stack
01001288 pop     r15d                       ; restore
0100128a pop     r14d                       ; restore
0100128c pop     r13d                       ; restore
0100128e pop     r12d                       ; restore
01001290 pop     rdi                        ; restore
01001291 pop     rsi                        ; restore
01001292 pop     rbx                        ; restore
01001293 ret                                ; return (do not pop arguments)
```

戻り値が格納されている**rax**、非 volatile レジスタを返す前に復元します。

 

 





