---
title: UMDH を使用してユーザー モードのメモリ リークを検出するには
description: UMDH を使用してユーザー モードのメモリ リークを検出するには
ms.assetid: b15ed695-3f35-4a72-93ab-3cbfd2e33980
keywords:
- メモリ リークが発生する場合、ユーザー モードの UMDH
- UMDH、メモリ リークの検出
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f215d8e02eeee80cc4a38a80b61a423c9c86d7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535307"
---
# <a name="using-umdh-to-find-a-user-mode-memory-leak"></a>UMDH を使用してユーザー モードのメモリ リークを検出するには


ユーザー モード ダンプのヒープ (UMDH) ユーティリティは、特定のプロセス用の Windows ヒープ割り当てを分析するオペレーティング システムで動作します。 UMDH を検索するルーチンでは、特定のプロセスはメモリ リークが発生します。

Windows ツールをデバッグには UMDH が含まれます。 完全な詳細については、[UMDH](umdh.md)を参照してください。

### <a name="span-idpreparingtouseumdhspanspan-idpreparingtouseumdhspanpreparing-to-use-umdh"></a><span id="preparing_to_use_umdh"></span><span id="PREPARING_TO_USE_UMDH"></span>UMDH を使用する準備

されませんが既に決まっているどのプロセスがメモリをリークしている場合、最初の操作を行います。 詳細については、[パフォーマンス モニターは、ユーザー モード メモリ リークの検出を使用して](using-performance-monitor-to-find-a-user-mode-memory-leak.md)を参照してください。

UMDH ログの最も重要なデータは、ヒープ割り当てのスタック トレースです。 プロセスがヒープのメモリをリークしているかどうかを確認するのには、これらのスタック トレースを分析します。

スタック トレース データを表示する UMDH を使用する前に使用する必要があります[GFlags](gflags.md)システムを適切に構成します。 Windows ツールをデバッグには GFlags が含まれます。

次の GFlags 設定は、UMDH スタック トレースを有効にします。

-   GFlags、グラフィカル インターフェイスでイメージ ファイル タブを選択して、(ファイル名拡張子を含む)、プロセス名を入力、選択、TAB キーを押す**ユーザー モードのスタック トレースのデータベースの作成**、 をクリックし、**適用**.

    または、同等に、次の GFlags コマンドラインを使用している*ImageName* (ファイル名拡張子を含む)、プロセス名には。

    ```dbgcmd
    gflags /i ImageName +ust 
    ```
    完了したら、GFlag 設定を消去するのにには、このコマンドを使用します。 詳細については、[GFlags コマンド](gflags-commands.md)を参照してください。

    ```dbgcmd
    gflags /i ImageName -ust 
    ```
    

-   Windows を収集するスタック トレース データの量が x86 32 MB に制限は既定では、プロセッサ、および 64 MB、x64 プロセッサ。 このデータベースのサイズを大きく必要があります場合、選択、**イメージ ファイル**GFlags グラフィック インターフェイスで タブで、プロセス名を入力、タブ キー、チェックを押して、 **Stack Backtrace (メガバイト)**  チェック ボックスを入力クリックして、関連付けられているテキスト ボックス内の値 (単位は MB)**適用**します。 限られた Windows リソースが消費されますが、ため、必要な場合にのみ、このデータベースが向上します。 サイズが大きくなる必要がなくなったには、元の値にこの設定を返します。

-   フラグのいずれかを変更した場合、**システム レジストリ** タブで、これらの変更を有効にする Windows を再起動する必要があります。 フラグのいずれかを変更した場合、**イメージ ファイル** タブで、変更を有効にするプロセスを再起動する必要があります。 変更、**カーネル フラグ** タブは、すぐに有効なが、失われた、次回の Windows を再起動します。

UMDH を使用する前に、アプリケーションの適切なシンボルへのアクセスが必要です。 UMDH 環境変数で指定されたシンボル パスを使用して\_NT\_シンボル\_パス。 この変数に格納をアプリケーションのシンボルを含むパスに設定します。 Windows シンボルへのパスを含めることも、分析がより詳細な可能性があります。 このシンボル パスの構文は、デバッガーによって使用されるのと同じ詳細については、[シンボル パス](symbol-path.md)を参照してください。

たとえば、アプリケーションのシンボルは c:\\MySymbols として、c: を使用して、Windows シンボルのパブリックの Microsoft シンボル ストアを使用する場合\\MyCache、ダウン ストリームのストアとしては、次のコマンドを使用します。シンボル パスを設定するには。

```console
set _NT_SYMBOL_PATH=c:\mysymbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols 
```

さらに、正確な結果を保証するために BSTR のキャッシュを無効する必要があります。 これを行うには、1 (1) に等しい OANOCACHE の環境変数を設定します。 割り当てを追跡するアプリケーションを起動する前に、この設定を行います。

サービスによって行われた割り当てを追跡する必要がある場合は、システム環境変数として OANOCACHE を設定しを有効にするこの設定の Windows を再起動する必要があります。


### <a name="span-iddetectingincreasesinheapallocationswithumdhspanspan-iddetectingincreasesinheapallocationswithumdhspandetecting-increases-in-heap-allocations-with-umdh"></a><span id="detecting_increases_in_heap_allocations_with_umdh"></span><span id="DETECTING_INCREASES_IN_HEAP_ALLOCATIONS_WITH_UMDH"></span>UMDH でヒープ割り当て増加を検出します。

これらの準備を行った後は、プロセスのヒープの割り当てに関する情報をキャプチャ UMDH を使用できます。 これを行うには、次の手順を実行します。

1.  確認、 [ID (PID) を処理](finding-the-process-id.md)を調査するプロセス。

2.  UMDH を使用して、このプロセスでは、ヒープ メモリの割り当てを分析し、ログ ファイルに保存します。 PID、およびログ ファイルの名前を持つ-f スイッチ-p スイッチを使用します。 たとえば、PID は 124、Log1.txt ログ ファイルの名前を付ける場合は、次のコマンドを使用します。

    ```console
    umdh -p:124 -f:log1.txt 
    ```dbgcmd

3.  Use Notepad or another program to open the log file. This file contains the call stack for each heap allocation, the number of allocations made through that call stack, and the number of bytes consumed through that call stack.

4.  Because you are looking for a memory leak, the contents of a single log file are not sufficient. You must compare log files recorded at different times to determine which allocations are growing.

    UMDH can compare two different log files and display the change in their respective allocation sizes. You can use the greater-than symbol (**&gt;**) to redirect the results into a third text file. You may also want to include the -d option, which converts the byte and allocation counts from hexadecimal to decimal. For example, to compare Log1.txt and Log2.txt, saving the results of the comparison to the file LogCompare.txt, use the following command:

    ```console
    umdh log1.txt log2.txt > logcompare.txt 
    ```

5.  LogCompare.txt ファイルを開きます。 その内容には、次のようになります。

    ```text
    + 5320 ( f110 - 9df0) 3a allocs BackTrace00B53 
    Total increase == 5320 
    ```

    各呼び出し履歴 (「バック トレース」というラベルが付いた) UMDH ログ ファイルで、2 つのログ ファイルの間で行われる比較があります。 この例では、最初はログ ファイル (Log1.txt) の 2 番目のログ ファイル記録 0xF110 のバイトまでの時間、2 つのログに割り当てられた 0x5320 追加のバイト数があることを意味する間に割り当てられた BackTrace00B53、記録された 0x9DF0 バイトがキャプチャされたです。 BackTrace00B53 で識別される呼び出し履歴からのバイトが付属しています。

6.  そのバック トレースで新機能を確認するには、元のログ ファイル (たとえば、Log2.txt) と"BackTrace00B53"を検索のいずれかを開く 結果は、このデータに似ています。

    ```text
    00005320 bytes in 0x14 allocations (@ 0x00000428) by: BackTrace00B53
    ntdll!RtlDebugAllocateHeap+0x000000FD
    ntdll!RtlAllocateHeapSlowly+0x0000005A
    ntdll!RtlAllocateHeap+0x00000808
    MyApp!_heap_alloc_base+0x00000069
    MyApp!_heap_alloc_dbg+0x000001A2
    MyApp!_nh_malloc_dbg+0x00000023
    MyApp!_nh_malloc+0x00000016
    MyApp!operator new+0x0000000E
    MyApp!DisplayMyGraphics+0x0000001E
    MyApp!main+0x0000002C
    MyApp!mainCRTStartup+0x000000FC
    KERNEL32!BaseProcessStart+0x0000003D 
    ```

    この UMDH 出力では、呼び出しスタックから割り当てられた合計バイト数を 0x5320 (10 進 21280) があったことを示しています。 これらのバイトが (10 進 1064) バイトに 0x428 の個別の割り当てを 0x14 (10 進数の 20) から割り当てられます。

    呼び出し履歴が"BackTrace00B53、"の識別子を指定された、このスタックに呼び出しが表示されます。 呼び出し履歴を確認するで、 **DisplayMyGraphics**ルーチンによってメモリの割り当ては、**新しい**演算子で、ルーチンを呼び出す*malloc*、使用します。ヒープからメモリを取得する Visual C ランタイム ライブラリ。

    これらの呼び出しは、ソース コードに明示的に表示される最後の 1 つを決定します。 この場合、これはおそらく、**新しい**演算子のため呼び出し*malloc*の実装の一環として発生**新しい**ではなく、個別の割り当て。 これのこのインスタンス、**新しい**演算子、 **DisplayMyGraphics**ルーチンは繰り返し解放されていないメモリの割り当て。

 

 





