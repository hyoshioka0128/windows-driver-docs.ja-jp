---
title: バグを発見する 12 の例を使用してヒープのページ検証
description: バグを発見する 12 の例を使用してヒープのページ検証
ms.assetid: aa3f5c53-8522-48be-a3cd-49b740803fe3
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a541f8ef5e454d73afebb0fd1ee48b251f453068
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529756"
---
# <a name="example-12-using-page-heap-verification-to-find-a-bug"></a>12 の例:ページ ヒープの検証を使用してバグを発見するには


## <span id="ddk_example_12___using_page_heap_verification_to_find_a_bug_dtools"></span><span id="DDK_EXAMPLE_12___USING_PAGE_HEAP_VERIFICATION_TO_FIND_A_BUG_DTOOLS"></span>


次の一連のコマンドでは、GFlags と NTSD デバッガーのページ ヒープの検証機能を使用して、ヒープ メモリの使用エラーを検出する方法を示します。 この例で、プログラマは疑わする架空のアプリケーション、pheap buggy.exe、ヒープ エラーが発生し、一連のエラーを識別するためのテストを実行します。

NTSD について詳しくは、[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)を参照してください。

### <a name="span-idstep1enablestandardpageheapverificationspanspan-idstep1enablestandardpageheapverificationspanspan-idstep1enablestandardpageheapverificationspanstep-1-enable-standard-page-heap-verification"></a><span id="Step_1__Enable_standard_page_heap_verification"></span><span id="step_1__enable_standard_page_heap_verification"></span><span id="STEP_1__ENABLE_STANDARD_PAGE_HEAP_VERIFICATION"></span>手順 1:標準的なページ ヒープの検証を有効にします。

次のコマンドにより、pheap の標準的なページ ヒープの検証-buggy.exe:

```console
gflags /p /enable pheap-buggy.exe
```

### <a name="span-idstep2verifythatpageheapisenabledspanspan-idstep2verifythatpageheapisenabledspanspan-idstep2verifythatpageheapisenabledspanstep-2-verify-that-page-heap-is-enabled"></a><span id="Step_2__Verify_that_page_heap_is_enabled"></span><span id="step_2__verify_that_page_heap_is_enabled"></span><span id="STEP_2__VERIFY_THAT_PAGE_HEAP_IS_ENABLED"></span>手順 2:そのページ ヒープが有効になっていることを確認します。

次のコマンドでは、ヒープのページ検証が有効になっているイメージ ファイルが表示されます。

```console
gflags /p
```

応答、GFlags は、次のプログラムの一覧を表示します。 この画面で、**トレース**標準ページ ヒープの検証を示すと**完全なトレース**完全ページ ヒープの検証を示します。 Pheap buggy.exe が記載されているこの例では、**トレース**、意図したとおり、標準的なページ ヒープの検証が有効になっていることを示します。

```console
pheap-buggy.exe: page heap enabled with flags (traces )
```

### <a name="span-idstep3runthedebuggerspanspan-idstep3runthedebuggerspanspan-idstep3runthedebuggerspanstep-3-run-the-debugger"></a><span id="Step_3__Run_the_debugger"></span><span id="step_3__run_the_debugger"></span><span id="STEP_3__RUN_THE_DEBUGGER"></span>手順 3:デバッガーを実行します。

次のコマンドを実行、 **CorruptAfterEnd** pheap-buggy.exe で NTSD での関数、 **-g** (最初のブレークポイントを無視する) と **-x** (セカンド チャンスの中断に設定アクセス違反例外) のパラメーター:

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

NTSD アプリケーションが失敗すると、次の表示は pheap でエラーが検出されたことを示しますが生成されます-buggy.exe:

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

ヘッダー情報が破損したブロックをヒープのアドレスが含まれています (00 C 81000。ヒープのハンドル)、破損したブロックのアドレス (00D81EB0:ヒープ ブロック)、および割り当てのサイズ (00000100。ブロック サイズの場合)。

「破損したサフィックス パターン」メッセージは、アプリケーションが GFlags が pheap buggy.exe ヒープ割り当ての終了後に挿入されたデータの整合性のパターンに違反したことを示します。

### <a name="span-idstep4displaythecallstackspanspan-idstep4displaythecallstackspanspan-idstep4displaythecallstackspanstep-4-display-the-call-stack"></a><span id="Step_4__Display_the_call_stack"></span><span id="step_4__display_the_call_stack"></span><span id="STEP_4__DISPLAY_THE_CALL_STACK"></span>手順 4:呼び出し履歴を表示します。

次の手順で、エラーの原因となった関数を検索する NTSD を報告したアドレスを使用します。 次の 2 つのコマンドでは、行番号の表示の行番号、呼び出し履歴、デバッガーでのダンプを有効にします。

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

その結果、デバッガーでは、行番号を pheap buggy.exe の呼び出し履歴を表示します。 呼び出し履歴の表示を示しますエラー発生したときに、 **TestCorruptAfterEnd** pheap buggy.exe で関数が呼び出すことによって 0x00c80000 で割り当てを解放しよう**選択肢**へのリダイレクト**RtlFreeHeap**します。

このエラーの最も可能性の高い原因は、この関数では、割り当てられているバッファーの末尾を越えたプログラムが記述したことです。

### <a name="span-idstep5enablefullpageheapverificationspanspan-idstep5enablefullpageheapverificationspanspan-idstep5enablefullpageheapverificationspanstep-5-enable-full-page-heap-verification"></a><span id="Step_5__Enable_full_page_heap_verification"></span><span id="step_5__enable_full_page_heap_verification"></span><span id="STEP_5__ENABLE_FULL_PAGE_HEAP_VERIFICATION"></span>手順 5:完全ページ ヒープの検証を有効にします。

標準的なページ ヒープの検証とは異なり完全ページ ヒープの検証は発生するとすぐにこのヒープ バッファーの誤用をキャッチできます。 次のコマンドにより、pheap の完全ページ ヒープの検証-buggy.exe:

```console
gflags /p /enable pheap-buggy.exe /full
```

### <a name="span-idstep6verifythatfullpageheapisenabledspanspan-idstep6verifythatfullpageheapisenabledspanspan-idstep6verifythatfullpageheapisenabledspanstep-6-verify-that-full-page-heap-is-enabled"></a><span id="Step_6__Verify_that_full_page_heap_is_enabled"></span><span id="step_6__verify_that_full_page_heap_is_enabled"></span><span id="STEP_6__VERIFY_THAT_FULL_PAGE_HEAP_IS_ENABLED"></span>手順 6:その完全ページ ヒープが有効になっていることを確認します。

次のコマンドには、ヒープのページ検証が有効になっているプログラムが一覧表示されます。

```console
gflags /p
```

応答、GFlags は、次のプログラムの一覧を表示します。 この画面で、**トレース**標準ページ ヒープの検証を示すと**完全なトレース**完全ページ ヒープの検証を示します。 Pheap buggy.exe が記載されているこの例では、**完全なトレース**、意図したとおり完全ページ ヒープの検証が有効になっていることを示します。

```console
pheap-buggy.exe: page heap enabled with flags (full traces )
```

### <a name="span-idstep7runthedebuggeragainspanspan-idstep7runthedebuggeragainspanspan-idstep7runthedebuggeragainspanstep-7-run-the-debugger-again"></a><span id="Step_7__Run_the_debugger_again"></span><span id="step_7__run_the_debugger_again"></span><span id="STEP_7__RUN_THE_DEBUGGER_AGAIN"></span>手順 7:デバッガーをもう一度実行します。

次のコマンドを実行、 **CorruptAfterEnd** pheap-buggy.exe NTSD デバッガーでの関数、 **-g** (最初のブレークポイントを無視する) と **-x** (設定アクセス違反例外でのセカンド チャンス中断) のパラメーター。

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

NTSD アプリケーションが失敗すると、次の表示は pheap でエラーが検出されたことを示しますが生成されます-buggy.exe:

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

完全ページ ヒープの検証が有効になっている、デバッガーは、アクセス違反で中断されます。 アクセス違反の正確な場所を検索するには、行番号のダンプを有効にして、コール スタック トレースを表示します。

番号付きのコール スタック トレースは次のようです。問題を表示する行は、太字で表示されます。

```console
ChildEBP RetAddr  Args to Child
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x1f [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 184]
0006ff4c 0100157f 00000002 00c16fd0 00b70eb0 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

行 184 pheap buggy.exe で問題が発生するスタック トレースを示しています。 完全ページ ヒープの検証が有効になっているため、呼び出し履歴は、システム DLL ではなく、プログラム コードで開始します。 その結果、違反は、これが発生した場合、ヒープ ブロックが解放されたのではなく検出されました。

### <a name="span-idstep8locatetheerrorinthecodespanspan-idstep8locatetheerrorinthecodespanspan-idstep8locatetheerrorinthecodespanstep-8-locate-the-error-in-the-code"></a><span id="Step_8__Locate_the_error_in_the_code"></span><span id="step_8__locate_the_error_in_the_code"></span><span id="STEP_8__LOCATE_THE_ERROR_IN_THE_CODE"></span>手順 8:コードで、エラーを見つけてください。

クイック検査では、問題の原因が表示されます。プログラムは、256 バイトの (0x100) バッファーの一般的なものではオフ エラー 257 バイト (0x101) への書き込みを試みます。

```console
*((PCHAR)Block + 0x100) = 0;
```

 

 





