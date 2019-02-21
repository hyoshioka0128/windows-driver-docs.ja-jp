---
title: その他の検査
description: その他の検査
ms.assetid: 4d7b14ae-5a3a-49b4-9678-6527cbacc4d4
keywords:
- その他の検査 WDK Driver Verifier をオプションします。
- lookasides WDK Driver Verifier
- 解放されたメモリ WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b151f493ec60ab921f3c675ff3e5b0def93c86dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556455"
---
# <a name="miscellaneous-checks"></a>その他の検査


Driver Verifier の他の確認オプションのドライバーをドライバーまたはシステムのアクティブなカーネル オブジェクトがまだ含まれているメモリの解放などのクラッシュが発生する一般的なエラーを監視します。

具体的には、その他のチェックのオプションは、次の不適切なドライバーの動作を探します。

-   **解放されたメモリのアクティブな作業項目です。** ドライバー呼び出し[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)を使用してキューに配置された作業項目を含むプールのブロックを解放する[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466). (このチェックは、Windows Server 2003 のチェック ビルドでは既定で有効です)。

-   **解放されたメモリ内のアクティブなリソース。** ドライバー呼び出し[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590) active を含むプールのブロックを解放する[÷ リソース構造](https://msdn.microsoft.com/library/windows/hardware/ff544281)します。 ドライバーを呼び出す必要があります[ **ExDeleteResource** ](https://msdn.microsoft.com/library/windows/hardware/ff544572)を呼び出す前に次のオブジェクトを削除する**ExFreePool**します。

-   **内のアクティブなルック アサイド リストには、メモリが解放されます。** ドライバー呼び出し[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590) active ルック アサイド リストがまだ含まれているプールのブロックを解放する ([**NPAGED\_ルック アサイド\_]ボックスの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff556431)または[**ページ\_ルック アサイド\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff558775)構造体。 ドライバーを呼び出す必要があります[ **ExDeleteNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544566)または[ **ExDeletePagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544570)リストするには、ルック アサイドの削除呼び出しの前に**ExFreePool**します。

-   **Windows Management Instrumentation (WMI) および Event Tracing for Windows (ETW) の登録の問題。** ドライバーの検証ツールによって検出されたこのような問題は次のとおりです。
    -   その WMI コールバックの登録を解除せずにアンロードしようとするドライバー。
    -   WMI から登録解除されていないデバイス オブジェクトを削除しようとするドライバー。
    -   その ETW カーネル モード プロバイダーの登録を解除せずにアンロードしようとするドライバー。
    -   既に登録されていないプロバイダーの登録を解除しようとするドライバー。
-   **カーネル ハンドル エラー。** (Windows Vista およびそれ以降のバージョン)その他の確認オプションを有効にすると、カーネル ハンドルのリークの調査に支援するために、システム プロセスのハンドルのトレースはこともでき、 [ **0x93 のバグ チェック。無効な\_カーネル\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff559292)します。 カーネル ハンドルのトレースが有効になっている、スタック トレースの収集は最近のハンドルを開くおよび閉じる操作。 スタック トレースを使用してカーネル デバッガーに表示できる、 **! htrace**デバッガー拡張機能。 詳細については **! htrace**ツールを Windows のデバッグ ドキュメントを参照してください。

-   **カーネル モードへのアクセスをユーザー モード ハンドル**以降、Windows 7 では、その他の確認オプションを選択すると、ドライバーの検証もチェックへの呼び出しに[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679). カーネル モードへのアクセスをユーザー モードのハンドルを渡すことはできません。 このような操作が発生した場合、Driver Verifier は 0xF6 のパラメーター 1 の値を持つバグ チェック 0xC4 を発行します。

-   **カーネル スタックに割り当てられた同期オブジェクトのユーザー モードの待機**

    Driver Verifier は、Windows 7 以降で、ドライバーは不正に使用して、オペレーティング システムを提供するマルチ スレッドの同期機構の他の方法を検出できます。

    カーネル スタック上のローカル変数として KEVENT 構造体などの同期オブジェクトの割り当ては、一般的な方法です。 プロセスがメモリに読み込まれて、中に、カーネル スタック、スレッドのことはありませんワーキング セットから除去されるか、ディスクにページ アウト。 このような非ページ メモリの同期オブジェクトの割り当てが正しいです。

    ただし、ときにドライバー Api を呼び出すよう[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)または[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)であるオブジェクトを待機するには指定する必要があります、スタックに割り当て、 **kernelmode である**API の値*WaitMode*パラメーター。 プロセスのすべてのスレッドが待機しているとき**UserMode**モード、プロセスが、ディスクにスワップ アウトする対象となります。 そのため場合、指定されたドライバー **UserMode**として、 *WaitMode*パラメーター、オペレーティング システムを入れ替えることも、現在のプロセスと同じプロセス内で他のすべてのスレッドが待機している限り、 **UserMode**もします。 ディスクにアウト プロセス全体をスワップすると、そのカーネル スタックをページングが含まれています。 オペレーティング システムにスワップ アウトする同期オブジェクトで待機しているが正しくありません。 ある時点で、スレッドが登場しと、同期オブジェクトを通知する必要があります。 IRQL でオブジェクトを操作する Windows カーネルは、同期オブジェクトがシグナル通知ディスパッチ =\_レベルまたはそれ以降。 ページ アウトをタッチまたはメモリのディスパッチに取り替える\_レベル、またはシステムの結果の上にクラッシュします。

    Driver Verifier チェック以降、Windows 7 ではその他の確認オプションを選択すると、同期での待機中に検証済みのドライバーを使用するオブジェクト**UserMode**は現在のスレッドのカーネルに割り当てられていませんスタックです。 発行 Driver Verifier は、このような不適切な待機を検出すると、 [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)パラメーター 1 値は 0x123 です。

-   **不適切なカーネル ハンドルの参照**

    各 Windows プロセス ハンドル テーブルがあります。 ハンドルのエントリの配列としてハンドル テーブルを表示できます。 有効なハンドルの各値は、この配列内の有効なエントリを参照します。

    A*カーネル ハンドル*として、システム プロセスのハンドル テーブルに対して有効なハンドル。 A*ユーザーのハンドル*として、システム プロセスを除く任意のプロセスに対して有効なハンドル。

    Windows 7 では、Driver Verifier は、カーネルを参照する試行が正しくない値の処理を検出します。 これらのドライバーの欠陥として報告される、 [ **0x93 のバグ チェック。無効な\_カーネル\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff559292)ドライバー検証ツールの他のチェックのオプションが有効になっている場合。 通常、ドライバーが既にそのハンドルを閉じていますが、使用を継続しようとして、この種の不適切なハンドルの参照を意味します。 参照されているハンドルの値が再利用された既に別の関連のないドライバーによって、この種の問題はシステムの予期しない問題の可能性します。

    カーネル ドライバーがカーネル ハンドルが最近閉じたレビュー、閉じられたハンドルを後で参照する場合、ドライバーの検証ツールは、前述のようバグ チェックを強制します。 この場合の出力、 [ **! htrace** ](https://msdn.microsoft.com/library/windows/hardware/ff563208)デバッガー拡張機能は、このハンドルを終了するコード パスのスタック トレースを提供します。 システム プロセスのアドレスを使用して、パラメーターとして **! htrace**します。 システム プロセスのアドレスを検索するには、使用、 **! 処理 4 0**コマンド。

    Windows 7 以降、Driver Verifier の追加のチェックを[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)します。 Kernelmode であるアクセス権を持つユーザー スペースのハンドルを渡すに禁止されているようになりました。 このような組み合わせが検出されると、ドライバーの検証ツール発行[ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)0xF6 のパラメーター 1 の値。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの他の確認オプションをアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    によって表されるその他の確認オプションをコマンドラインで**ビット 11 (0x800)** します。 その他のチェックを有効にするには、0x800 のフラグの値を使用して、または 0x800 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x800 /driver MyDriver.sys
    ```

    オプションは、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンでもアクティブ化し、追加することで、コンピューターを再起動しなくてもその他のチェックを非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x800 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    その他のチェックのオプションは、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier  /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**、順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択**その他の検査**します。

    その他のチェック機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果を表示します。

その他の確認オプションの結果を表示する、 **! verifier**カーネル デバッガーでの拡張機能。 (について **! verifier**を参照してください、*ツールを Windows のデバッグ*ドキュメントです)。

次の例では、その他の確認オプションが検出されました、ドライバーが、解放しようとしていたメモリ内のアクティブなスケジュール作成構造体で[ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)します。 バグ チェック 0xC4 表示には、スケジュールを作成し、影響を受けるメモリのアドレスが含まれています。

```
1: kd> !verifier 1

Verify Level 800 ... enabled options are:
 Miscellaneous checks enabled

Summary of All Verifier Statistics

RaiseIrqls                             0x0
AcquireSpinLocks                       0x0
Synch Executions                       0x0
Trims                                  0x0

Pool Allocations Attempted             0x1
Pool Allocations Succeeded             0x1
Pool Allocations Succeeded SpecialPool 0x0
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x0
Resource Allocations Failed Deliberately   0x0

Current paged pool allocations         0x0 for 00000000 bytes
Peak paged pool allocations            0x0 for 00000000 bytes
Current nonpaged pool allocations      0x0 for 00000000 bytes
Peak nonpaged pool allocations         0x0 for 00000000 bytes

Driver Verification List

Entry     State           NonPagedPool   PagedPool   Module

8459ca50 Loaded           00000000       00000000    buggy.sys



*** Fatal System Error: 0x000000c4
 (0x000000D2,0x9655D4A8,0x9655D468,0x000000B0)


        0xD2 : Freeing pool allocation that contains active ERESOURCE.
               2 -  ERESOURCE address.
               3 -  Pool allocation start address.
               4 -  Pool allocation size.
```

プールの割り当てを調査するために使用して、 [ **! プール**](https://msdn.microsoft.com/library/windows/hardware/ff564691)デバッガー 9655D 468、プールの割り当ての開始アドレスと拡張機能。 (、 *2*フラグが指定されたアドレスを格納するプールに関してのみ、ヘッダー情報が表示されます。 他のプールのヘッダー情報は表示されません。)

```
1: kd> !pool 9655d468  2
Pool page 9655d468 region is Paged pool
*9655d468 size:   b0 previous size:    8  (Allocated) *Bug_
```

については、次を検索するには使用、 [ **! ロック (! kdext\*.locks)** ](https://msdn.microsoft.com/library/windows/hardware/ff563980)デバッガー拡張機能、構造体のアドレスを使用します。

```
1: kd> !locks 0x9655D4A8     <<<<<- ERESOURCE @0x9655D4A8 lives inside the pool block being freed

Resource @ 0x9655d4a8    Available
1 total locks
```

使用することも、 **kb**デバッガー コマンドを呼び出し、失敗の原因となったのスタック トレースを表示します。 次の例は、スタックは呼び出しを含む、 **ExFreePoolWithTag**その Driver Verifier をインターセプトします。

```
1: kd> kb
ChildEBP RetAddr  Args to Child
92f6374c 82c2c95a 00000003 92f68cdc 00000000 nt!RtlpBreakWithStatusInstruction 
92f6379c 82c2d345 00000003 9655d468 000000c4 nt!KiBugCheckDebugBreak+0x1c 
92f63b48 82c2c804 000000c4 000000d2 9655d4a8 nt!KeBugCheck2+0x5a9 
92f63b6c 82e73bae 000000c4 000000d2 9655d4a8 nt!KeBugCheckEx+0x1e 
92f63b88 82e78c32 9655d4a8 9655d468 000000b0 nt!VerifierBugCheckIfAppropriate+0x3c 
92f63ba4 82ca7dcb 9655d468 000000b0 00000000 nt!VfCheckForResource+0x52 
92f63bc8 82e7fb2d 000000b0 00000190 9655d470 nt!ExpCheckForResource+0x21 
92f63be4 82e6dc6c 9655d470 92f63c18 89b6c58c nt!ExFreePoolSanityChecks+0x1fb 
92f63bf0 89b6c58c 9655d470 00000000 89b74194 nt!VerifierExFreePoolWithTag+0x28 
92f63c00 89b6c0f6 846550c8 846550c8 846e2200 buggy!MmTestProbeLockForEverStress+0x2e 
92f63c18 82e6c5f1 846e2200 846550c8 85362e30 buggy!TdDeviceControl+0xc4 
92f63c38 82c1fd81 82d4d148 846550c8 846e2200 nt!IovCallDriver+0x251 
92f63c4c 82d4d148 85362e30 846550c8 84655138 nt!IofCallDriver+0x1b 
92f63c6c 82d4df9e 846e2200 85362e30 00000000 nt!IopSynchronousServiceTail+0x1e6 
92f63d00 82d527be 00000001 846550c8 00000000 nt!IopXxxControlFile+0x684 
92f63d34 82cb9efc 0000004c 00000000 00000000 nt!NtDeviceIoControlFile+0x2a 
92f63d34 6a22b204 0000004c 00000000 00000000 nt!KiFastCallEntry+0x12c 
```

 

 





