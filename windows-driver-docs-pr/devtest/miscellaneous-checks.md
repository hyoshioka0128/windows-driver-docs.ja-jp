---
title: その他の検査
description: その他の検査
ms.assetid: 4d7b14ae-5a3a-49b4-9678-6527cbacc4d4
keywords:
- その他のチェックオプション WDK Driver Verifier
- look aside WDK Driver Verifier
- 解放されたメモリ WDK ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94456735bd9ea79d3d8b1139d8733bea3457ecb
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999069"
---
# <a name="miscellaneous-checks"></a>その他の検査


ドライバーの検証ツールの [その他のチェック] オプションは、ドライバーまたはシステムがクラッシュする原因となる一般的なエラーを監視します。たとえば、アクティブなカーネルオブジェクトがまだ含まれているメモリを解放します。

具体的には、[その他のチェック] オプションを選択すると、次の不適切なドライバーの動作が検索されます。

-   **解放されたメモリ内のアクティブな作業項目。** ドライバーは[**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出して、 [**ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)を使用してキューに登録された作業項目を含むプールブロックを解放します。 

-   **解放されたメモリ内のアクティブなリソース。** ドライバーは、 [**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出して、アクティブなリソース[構造](https://docs.microsoft.com/windows-hardware/drivers/kernel/eresource-structures)を含むプールブロックを解放します。 ドライバーは、 [**ExDeleteResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)を呼び出して、リソースオブジェクトを削除してから、 **exfreepool**を呼び出す必要があります。

-   **解放されたメモリ内のアクティブなルックアサイドリスト。** ドライバーは、 [**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出して、アクティブなルックアサイドリスト ([**\_\_Npaged ルックアサイド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)リストまたは[**ページ\_ルック\_アサイドリスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造) がまだ含まれているプールブロックを解放します。 ドライバーは、 [**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)または[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)を呼び出して、 **exfreepool**を呼び出す前にルックアサイドリストを削除する必要があります。

-   **Windows Management Instrumentation (WMI) と Windows イベントトレーシング (ETW) の登録に関する問題。** ドライバーの検証ツールで検出されるこのような問題を次に示します。
    -   WMI コールバックの登録を解除せずに、アンロードを試みるドライバー。
    -   WMI から登録解除されていないデバイスオブジェクトを削除しようとするドライバー。
    -   ETW カーネルモードプロバイダーを登録解除せずにアンロードを試みるドライバー。
    -   既に登録が解除されているプロバイダーの登録を解除しようとするドライバー。
-   **カーネルハンドルエラー。** (Windows Vista 以降のバージョン)[その他のチェック] オプションを有効にすると、システムプロセスのハンドルトレースも有効になり、カーネルハンドルのリークと[**バグチェック 0x93: 無効\_なカーネル\_ハンドル**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x93--invalid-kernel-handle)を調べることができます。 ハンドルトレースが有効になっている場合、カーネルは最近のハンドルのオープンおよびクローズ操作のスタックトレースを収集します。 スタックトレースは、 **! htrace**デバッガー拡張機能を使用してカーネルデバッガーに表示できます。 **! Htrace**の詳細については、Windows 用デバッグツールのドキュメントを参照してください。

-   **カーネルモードアクセスを使用したユーザーモードハンドル**Windows 7 以降では、[その他のチェック] オプションを選択すると、ドライバー検証ツールによって[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)の呼び出しもチェックされます。 カーネルモードのアクセス権を持つユーザーモードハンドルを渡すことはできません。 このような操作が発生した場合、ドライバーの検証ツールは、パラメーター1の値が0xF6 のバグチェック0xC4 を発行します。

-   **モードでカーネルスタックに割り当てられた同期オブジェクトを待機する**

    Windows 7 以降では、ドライバーの検証ツールは、オペレーティングシステムによって提供されるマルチスレッド同期機構をドライバーが誤って使用することを検出できます。

    KEVENT 構造体などの同期オブジェクトをカーネルスタック上のローカル変数として割り当てることは、一般的な方法です。 プロセスがメモリに読み込まれている間、そのスレッドのカーネルスタックはワーキングセットからトリミングされることも、ディスクにページングされることもありません。 このような非ページングメモリ内の同期オブジェクトの割り当ては正しいです。

    ただし、ドライバーが[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)や[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)などの api を呼び出して、スタックに割り当てられたオブジェクトを待機する場合は、api の*waitmode*パラメーターに**kernelmode で**値を指定する必要があります。 プロセスのすべてのスレッド**がモードモードで待機**している場合、そのプロセスはディスクにスワップアウトできる状態になります。 そのため、ドライバーで*Waitmode*パラメーターとし**てモードが指定さ**れている場合、同じプロセス内の他のすべてのスレッドが非アクティブ**状態とし**て待機している限り、オペレーティングシステムは現在のプロセスをスワップアウトできます。 プロセス全体をディスクにスワップすると、そのカーネルスタックがページングされます。 オペレーティングシステムがスワップアウトした同期オブジェクトを待機していますが、正しくありません。 ある時点で、スレッドを取得し、同期オブジェクトを通知する必要があります。 同期オブジェクトをシグナリングするには、IRQL = ディスパッチ\_レベル以上でオブジェクトを操作する Windows カーネルが必要です。 ディスパッチ\_レベル以上でページングされたメモリをタッチしたり、スワップアウトしたりすると、システムがクラッシュします。

    Windows 7 以降では、[その他のチェック] オプションを選択すると、ドライバーの検証ツールは、検証されたドライバーがユーザー**モード**で待機するために使用する同期オブジェクトが、現在のスレッドのカーネルスタックに割り当てられていないことを確認します。 ドライバーの検証ツールが間違った待機を検出すると、[**バグチェック 0xC4:\_ドライバー\_検証\_ツールが検出さ**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)れ、パラメーター1の値が0x123 であることを確認します。

-   **無効なカーネルハンドル参照**

    各 Windows プロセスには、ハンドルテーブルがあります。 ハンドルテーブルをハンドルエントリの配列として表示できます。 有効な各ハンドル値は、この配列内の有効なエントリを参照します。

    システムプロセスのハンドルテーブルに対して有効なハンドルとしての*カーネルハンドル*。 システムプロセス以外のすべてのプロセスに対して有効なハンドルとしての*ユーザーハンドル*。

    Windows 7 では、ドライバーの検証ツールは、正しくないカーネルハンドル値を参照しようとします。 これらのドライバーの欠陥は、[**バグチェック 0x93\_\_**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x93--invalid-kernel-handle)として報告されます。 Driver Verifier のその他のチェックオプションが有効になっている場合は、無効なカーネルハンドルです。 通常、この種の不適切なハンドル参照とは、ドライバーが既にハンドルを閉じていても、その使用を継続しようとしていることを意味します。 この種の欠陥により、参照されているハンドル値が別の関連のないドライバーによって既に再利用されている可能性があるため、システムに対して予期しない問題が発生する可能性があります。

    カーネルドライバーが最近カーネルハンドルを閉じ、後で closed ハンドルを参照した場合、ドライバーの検証ツールは、前述のようにバグチェックを強制的に実行します。 この場合、 [**! htrace**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-htrace)デバッガー拡張機能の出力によって、このハンドルを閉じたコードパスのスタックトレースが提供されます。 **! Htrace**のパラメーターとしてシステムプロセスのアドレスを使用します。 システムプロセスのアドレスを確認するには、 **! process 4 0**コマンドを使用します。

    Windows 7 以降では、ドライバーの検証ツールによって[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)にチェックが追加されます。 Kernelmode で access を使用してユーザー空間ハンドルを渡すことが禁止されました。 このような組み合わせが検出された場合、ドライバーの検証ツールは[**バグ\_チェック\_0xc4: ドライバー\_検証ツールが違反を検出**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)し、パラメーター1の値が0xf6 であることを確認します。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーのその他のチェックオプションをアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、[その他のチェック] オプションは**ビット 11 (0x800)** で表されます。 その他のチェックをアクティブにするには、フラグ値を0x800 にするか、フラグ値に0x800 を追加します。 次に例を示します。

    ```
    verifier /flags 0x800 /driver MyDriver.sys
    ```

    オプションは、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動せずに、その他のチェックをアクティブ化および非アクティブ化することもできます。 次に例を示します。

    ```
    verifier /volatile /flags 0x800 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    [その他のチェック] オプションも、標準設定に含まれています。 次に例を示します。

    ```
    verifier  /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、[**次へ**] をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  [**その他のチェック**] を選択します。

    その他のチェック機能も、標準設定に含まれています。 この機能を使用するには、ドライバー検証マネージャーで [**標準設定の作成**] をクリックします。

### <a name="span-idviewing_the_resultsspanspan-idviewing_the_resultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果の表示

その他のチェックオプションの結果を表示するには、カーネルデバッガーで **! verifier**拡張機能を使用します。 ( **! Verifier**の詳細については、 *Windows 用デバッグツール*のドキュメントを参照してください)。

次の例では、[その他のチェック] オプションを選択すると、ドライバーが解放しようとしていたメモリ内のアクティブな作業の量が検出され、[**バグチェック 0xC4: ドライバー\_検証ツール\_の違反が検出\_**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)されました。 バグチェック0xC4 の表示には、÷のアドレスと影響を受けるメモリが含まれています。

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

プールの割り当てを調査するには、プールの割り当ての開始アドレス (9655D468) で[**! プール**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-pool)デバッガー拡張機能を使用します。 ( *2*フラグは、指定されたアドレスを含むプールのヘッダー情報のみを表示します。 他のプールのヘッダー情報は表示されません)。

```
1: kd> !pool 9655d468  2
Pool page 9655d468 region is Paged pool
*9655d468 size:   b0 previous size:    8  (Allocated) *Bug_
```

に関する情報を検索するには、構造体のアドレスを使用して、 [**! locks (! kdext\*. locks)**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-locks---kdext--locks-)デバッガー拡張機能を使用します。

```
1: kd> !locks 0x9655D4A8     <<<<<- ERESOURCE @0x9655D4A8 lives inside the pool block being freed

Resource @ 0x9655d4a8    Available
1 total locks
```

また、 **kb**デバッガーコマンドを使用して、エラーの原因となった呼び出しのスタックトレースを表示することもできます。 次の例は、ドライバーの検証ツールがインターセプトした**Exfreepoolwithtag**の呼び出しを含むスタックを示しています。

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

 

 





