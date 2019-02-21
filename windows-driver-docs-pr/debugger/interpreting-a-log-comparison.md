---
title: ログの比較を解釈します。
description: ログの比較を解釈します。
ms.assetid: fe2acdd5-00aa-4414-a59e-e6203ad48363
keywords:
- ログの比較を解釈する UMDH
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f223dab0c0d50915f715758a9302b53f6deb87b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552023"
---
# <a name="interpreting-a-log-comparison"></a>ログの比較を解釈します。


## <span id="ddk_interpreting_a_log_comparison_dtools"></span><span id="DDK_INTERPRETING_A_LOG_COMPARISON_DTOOLS"></span>


時間の経過と共に、同じプロセスの複数のユーザー モード ダンプ ヒープ (UMDH) ログを生成できます。 次に、ログを比較し、確認する呼び出しスタック割り当てが間の試用版を最大限に拡大 UMDH を使用できます。

たとえば、次のコマンドは UMDH Log1.txt と Log2.txt、2 つの UMDH ログを比較するよう指示し、Compare.txt、3 番目のファイルに出力をリダイレクトします。

```console
umdh -v Log1.txt Log2.txt > Compare.txt
```

結果として得られる Compare.txt ファイルは、各ログに記録された呼び出し履歴を一覧表示され、各スタックでは、ログ ファイルの間でヒープ割り当ての変更が表示されます。

たとえば、ファイルから次の行がその"Backtrace00053"というラベルの付いた呼び出し履歴内の関数の割り当てサイズの変化を示します

Log1.txt、40,432 (0x9DF0) (バイト単位) で、呼び出しスタックのアカウントで Log2.txt、同じコール スタックのアカウント 61,712 (0xF110) (バイト単位) 21,280 (0x5320) の相違 (バイト)。

```console
+ 5320 (f110 - 9df0) 3a allocs BackTrace00053 
Total increase == 5320
```

割り当てのスタックを次に示します。

```console
ntdll!RtlDebugAllocateHeap+0x000000FD
ntdll!RtlAllocateHeapSlowly+0x0000005A
ntdll!RtlAllocateHeap+0x00000808
MyApp!_heap_alloc_base+0x00000069
MyApp!_heap_alloc_dbg+0x000001A2
MyApp!_nh_malloc_dbg+0x00000023
MyApp!_nh_malloc+0x00000016
MyApp!operator new+0x0000000E
MyApp!LeakyFunc+0x0000001E
MyApp!main+0x0000002C
MyApp!mainCRTStartup+0x000000FC
KERNEL32!BaseProcessStart+0x0000003D
```

示しています、コール スタックの検査、**内容**関数は、Visual C ランタイム ライブラリを使用してメモリを割り当てることです。 その他のログ ファイルの検証が、割り当てが時間の経過と共に増大を最後に、ヒープから割り当てられているメモリできる場合がありますに表示されている場合は解放されているされません。

### <a name="span-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>ログ ファイルの分析のシンボル ファイル

2 台のコンピューターがあるとします。、*コンピューターへのログオン*UMDH ログを作成すると、*分析コンピューター* UMDH ログを分析します。 分析のコンピューター上のシンボル パスは、ログが行われた時にログ記録のコンピューターに読み込まれている Windows のバージョンのシンボルを指す必要があります。 シンボル サーバーを分析コンピューターにシンボル パスを指していません。 場合は、UMDH は分析のコンピューターで実行されている Windows のバージョンのシンボルを取得し、UMDH に意味のある結果は表示されません。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[UMDH を使用してユーザー モードのメモリ リークを検出するには](using-umdh-to-find-a-user-mode-memory-leak.md)

 

 





