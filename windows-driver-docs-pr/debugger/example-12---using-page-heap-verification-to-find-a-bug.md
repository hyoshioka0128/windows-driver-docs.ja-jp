---
title: ページヒープ検証を使用してバグを検出する例12
description: ページヒープ検証を使用してバグを検出する例12
ms.assetid: aa3f5c53-8522-48be-a3cd-49b740803fe3
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5dc76e4c73a8ce64b24b2506e1b38248724f7de0
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435377"
---
# <a name="example-12-using-page-heap-verification-to-find-a-bug"></a>例 12: ページヒープ検証を使用したバグの検出


## <span id="ddk_example_12___using_page_heap_verification_to_find_a_bug_dtools"></span><span id="DDK_EXAMPLE_12___USING_PAGE_HEAP_VERIFICATION_TO_FIND_A_BUG_DTOOLS"></span>


次の一連のコマンドは、GFlags および NTSD デバッガーのページヒープ検証機能を使用して、ヒープメモリ使用のエラーを検出する方法を示しています。 この例では、架空のアプリケーション pheap-buggy にはヒープエラーがあり、一連のテストを実行してエラーを特定します。

NTSD の詳細については、「 [CDB と Ntsd を使用](debugging-using-cdb-and-ntsd.md)したデバッグ」を参照してください。

### <a name="span-idstep_1__enable_standard_page_heap_verificationspanspan-idstep_1__enable_standard_page_heap_verificationspanspan-idstep_1__enable_standard_page_heap_verificationspanstep-1-enable-standard-page-heap-verification"></a><span id="Step_1__Enable_standard_page_heap_verification"></span><span id="step_1__enable_standard_page_heap_verification"></span><span id="STEP_1__ENABLE_STANDARD_PAGE_HEAP_VERIFICATION"></span>手順 1: 標準ページヒープの検証を有効にする

次のコマンドは、pheap-buggy の標準のページヒープ検証を有効にします。

```console
gflags /p /enable pheap-buggy.exe
```

### <a name="span-idstep_2__verify_that_page_heap_is_enabledspanspan-idstep_2__verify_that_page_heap_is_enabledspanspan-idstep_2__verify_that_page_heap_is_enabledspanstep-2-verify-that-page-heap-is-enabled"></a><span id="Step_2__Verify_that_page_heap_is_enabled"></span><span id="step_2__verify_that_page_heap_is_enabled"></span><span id="STEP_2__VERIFY_THAT_PAGE_HEAP_IS_ENABLED"></span>手順 2: ページヒープが有効になっていることを確認する

次のコマンドは、ページヒープ検証が有効になっているイメージファイルを一覧表示します。

```console
gflags /p
```

これに対して、GFlags は次のプログラムの一覧を表示します。 この画面では、**トレース**は標準のページヒープの検証を示し、**完全なトレース**はページヒープの完全な検証を示します。 この場合、pheap-buggy は**トレース**と共に一覧表示され、意図したとおりに標準ページヒープの検証が有効になっていることを示します。

```console
pheap-buggy.exe: page heap enabled with flags (traces )
```

### <a name="span-idstep_3__run_the_debuggerspanspan-idstep_3__run_the_debuggerspanspan-idstep_3__run_the_debuggerspanstep-3-run-the-debugger"></a><span id="Step_3__Run_the_debugger"></span><span id="step_3__run_the_debugger"></span><span id="STEP_3__RUN_THE_DEBUGGER"></span>手順 3: デバッガーを実行する

次のコマンドは、 **-g** (最初のブレークポイントを無視) および **-x** (アクセス違反例外に対して2回目を設定) パラメーターを使用して、pheap-buggy の**CorruptAfterEnd**関数を実行します。

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

アプリケーションに障害が発生すると、NTSD は次の表示を生成します。これは、pheap-buggy でエラーが検出されたことを示しています。

```dbgcmd
===========================================================
VERIFIER STOP 00000008: pid 0xAA0: corrupted suffix pattern

        00C81000 : Heap handle 
        00D81EB0 : Heap block 
        00000100 : Block size 
#         00000000 :
===========================================================

Break instruction exception - code 80000003 (first chance)
eax=00000000 ebx=00d81eb0 ecx=77f7e257 edx=0006fa18 esi=00000008 edi=00c81000
eip=77f7e098 esp=0006fc48 ebp=0006fc5c iopl=0         nv up ei pl zr na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000246
ntdll!DbgBreakPoint:
77f7e098 cc               int     3
```

ヘッダー情報には、破損したブロック (00C81000: ヒープハンドル) を持つヒープのアドレス、破損したブロックのアドレス (00D81EB0: Heap block)、および割り当てのサイズ (00000100: Block size) が含まれます。

"破損したサフィックスパターン" メッセージは、pheap-buggy ヒープ割り当ての終了後に、GFlags によって挿入されたデータ整合性パターンにアプリケーションが違反したことを示します。

### <a name="span-idstep_4__display_the_call_stackspanspan-idstep_4__display_the_call_stackspanspan-idstep_4__display_the_call_stackspanstep-4-display-the-call-stack"></a><span id="Step_4__Display_the_call_stack"></span><span id="step_4__display_the_call_stack"></span><span id="STEP_4__DISPLAY_THE_CALL_STACK"></span>手順 4: 呼び出し履歴を表示する

次の手順では、NTSD に報告されたアドレスを使用して、エラーの原因となった関数を見つけます。 次の2つのコマンドは、デバッガーで行番号のダンプを有効にし、行番号を含む呼び出し履歴を表示します。

```dbgcmd
C:\>.lines

Line number information will be loaded 

C:\>kb

ChildEBP RetAddr  Args to Child
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fc5c 77f9e6dd 00000008 77f9e3e8 00c81000 ntdll!DbgBreakPoint
0006fcd8 77f9f3c8 00c81000 00000004 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x2879
0006fcfc 77f9f5bb 00c81000 01001002 00000010 ntdll!RtlpNtEnumerateSubKey+0x3564
0006fd4c 77fa261e 00c80000 01001002 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x3757
0006fdc0 77fc0dc2 00c80000 01001002 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x67ba
0006fe78 77fbd87b 00c80000 01001002 00d81eb0 ntdll!RtlSizeHeap+0x16a8
0006ff24 010013a4 00c80000 01001002 00d81eb0 ntdll!RtlFreeHeap+0x69
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x2b [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 185]
0006ff4c 0100157f 00000002 00c65a68 00c631d8 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

その結果、デバッガーは pheap-buggy の呼び出し履歴を行番号と共に表示します。 呼び出し履歴の表示では、pheap-buggy の**TestCorruptAfterEnd**関数が**heapfree**を呼び出して0x00c80000 で割り当てを解放しようとしたときに、エラーが発生したことを示しています。 **rtlfreeheap**へのリダイレクトです。

このエラーの最も可能性が高い原因は、プログラムが、この関数で割り当てられたバッファーの末尾を越えて書き込んだことです。

### <a name="span-idstep_5__enable_full_page_heap_verificationspanspan-idstep_5__enable_full_page_heap_verificationspanspan-idstep_5__enable_full_page_heap_verificationspanstep-5-enable-full-page-heap-verification"></a><span id="Step_5__Enable_full_page_heap_verification"></span><span id="step_5__enable_full_page_heap_verification"></span><span id="STEP_5__ENABLE_FULL_PAGE_HEAP_VERIFICATION"></span>手順 5: ページヒープの完全な検証を有効にする

標準のページヒープ検証とは異なり、完全なページヒープ検証では、このヒープバッファーが発生するとすぐに誤用をキャッチすることができます。 次のコマンドを実行すると、pheap-buggy のページヒープの完全な検証が有効になります。

```console
gflags /p /enable pheap-buggy.exe /full
```

### <a name="span-idstep_6__verify_that_full_page_heap_is_enabledspanspan-idstep_6__verify_that_full_page_heap_is_enabledspanspan-idstep_6__verify_that_full_page_heap_is_enabledspanstep-6-verify-that-full-page-heap-is-enabled"></a><span id="Step_6__Verify_that_full_page_heap_is_enabled"></span><span id="step_6__verify_that_full_page_heap_is_enabled"></span><span id="STEP_6__VERIFY_THAT_FULL_PAGE_HEAP_IS_ENABLED"></span>手順 6: ページヒープ全体が有効になっていることを確認する

次のコマンドは、ページヒープ検証が有効になっているプログラムを一覧表示します。

```console
gflags /p
```

これに対して、GFlags は次のプログラムの一覧を表示します。 この画面では、**トレース**は標準のページヒープの検証を示し、**完全なトレース**はページヒープの完全な検証を示します。 この場合、pheap-buggy は**完全なトレース**と共に一覧表示され、完全なページヒープの検証が有効になっていることを示しています。

```console
pheap-buggy.exe: page heap enabled with flags (full traces )
```

### <a name="span-idstep_7__run_the_debugger_againspanspan-idstep_7__run_the_debugger_againspanspan-idstep_7__run_the_debugger_againspanstep-7-run-the-debugger-again"></a><span id="Step_7__Run_the_debugger_again"></span><span id="step_7__run_the_debugger_again"></span><span id="STEP_7__RUN_THE_DEBUGGER_AGAIN"></span>手順 7: デバッガーを再実行する

次のコマンドは、pheap-buggy の**CorruptAfterEnd**関数を、 **-g** (最初のブレークポイントを無視) および **-x** (アクセス違反例外に対して2回目の設定) パラメーターを使用して、NTSD デバッガーで実行します。

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

アプリケーションに障害が発生すると、NTSD は次の表示を生成します。これは、pheap-buggy でエラーが検出されたことを示しています。

```console
Page heap: process 0x5BC created heap @ 00880000 (00980000, flags 0x3)
ModLoad: 77db0000 77e8c000   kernel32.dll
ModLoad: 78000000 78046000   MSVCRT.dll
Page heap: process 0x5BC created heap @ 00B60000 (00C60000, flags 0x3)
Page heap: process 0x5BC created heap @ 00C80000 (00D80000, flags 0x3)
Access violation - code c0000005 (first chance)
Access violation - code c0000005 (!!! second chance !!!)
eax=00c86f00 ebx=00000000 ecx=77fbd80f edx=00c85000 esi=00c80000 edi=00c16fd0
eip=01001398 esp=0006ff2c ebp=0006ff4c iopl=0         nv up ei pl nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000206
pheap-buggy!TestCorruptAfterEnd+1f:
01001398 889801010000     mov     [eax+0x101],bl          ds:0023:00c87001=??
```

ページヒープの完全な検証が有効になっている場合、デバッガーはアクセス違反時に中断します。 アクセス違反の正確な場所を検索するには、行番号のダンプを有効にし、呼び出し履歴トレースを表示します。

番号付きコールスタックトレースは、次のように表示されます。 

```console
ChildEBP RetAddr  Args to Child
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x1f [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 184]
0006ff4c 0100157f 00000002 00c16fd0 00b70eb0 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

スタックトレースは、pheap-buggy の184行目で問題が発生していることを示しています。 ページヒープの完全な検証が有効になっているため、呼び出し履歴はシステム DLL ではなくプログラムコードで開始されます。 その結果、ヒープブロックが解放されたときではなく、違反が発生した場所でキャッチされました。

### <a name="span-idstep_8__locate_the_error_in_the_codespanspan-idstep_8__locate_the_error_in_the_codespanspan-idstep_8__locate_the_error_in_the_codespanstep-8-locate-the-error-in-the-code"></a><span id="Step_8__Locate_the_error_in_the_code"></span><span id="step_8__locate_the_error_in_the_code"></span><span id="STEP_8__LOCATE_THE_ERROR_IN_THE_CODE"></span>手順 8: コードでエラーを見つける

クイック検査では、問題の原因が明らかになります。プログラムは、一般的な1つずつのエラーである256バイト (0x100) バッファーの257th バイト (0x101) への書き込みを試みます。

```console
*((PCHAR)Block + 0x100) = 0;
```

 

 





