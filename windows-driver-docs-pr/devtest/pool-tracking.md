---
title: プールの追跡
description: プール追跡は、ドライバーによって行われたメモリ割り当てを監視します。
ms.assetid: 5b8aa775-d908-4a7a-b54f-6c63ac1ebd13
keywords:
- メモリプールの追跡機能 WDK ドライバーの検証ツール
- プールの追跡機能 WDK ドライバーの検証ツール
- メモリ割り当て WDK ドライバー検証ツール
- メモリリーク WDK ドライバー検証ツール
- 解放さメモリ割り当ての WDK ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae66b9778e17073525b152ef96c180d5fab8442d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840053"
---
# <a name="pool-tracking"></a>プールの追跡


プール追跡は、ドライバーによって行われたメモリ割り当てを監視します。 ドライバーがアンロードされた時点で、ドライバーの検証ツールは、ドライバーによって行われたすべての割り当てが解放されたことを保証します。

## <span id="ddk_memory_pool_tracking_tools"></span><span id="DDK_MEMORY_POOL_TRACKING_TOOLS"></span>


解放さのメモリ割り当て (*メモリリーク*とも呼ばれます) は、オペレーティングシステムのパフォーマンスを低下させる一般的な原因です。 システムプールをフラグメント化し、最終的にシステムクラッシュを引き起こす可能性があります。

このオプションがアクティブになっている場合、ドライバーの割り当てをすべて解放せずにドライバーがアンロードされると、ドライバーの検証ツールはバグチェック 0xC4 (パラメーター1が0x62 に等しい) を発行します。

Driver Verifier がこのバグチェックを発行する場合、パラメーター1が0x51、0x52、0x52、0x52、または0x52 と同じである場合、ドライバーは割り当ての外部のメモリに書き込まれています。 この場合は、[特別なプール](special-pool.md)機能を有効にして、エラーの原因を特定する必要があります。

バグチェックパラメーターの一覧については、「[**バグチェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (ドライバー\_VERIFIER\_検出された\_違反)」を参照してください。

Windows Vista 以降では、プール追跡オプションを有効にすると、ロックされたページの追跡も有効になります。 このオプションが有効になっていると、ドライバーが i/o 操作後にロックされたページの解放に失敗した場合に、ドライバーの検証ツールが[**バグチェック 0xCB**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xcb--driver-left-locked-pages-in-process) (ドライバー\_左\_ロックされている\_\_ページを\_プロセス) に発行します。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、プール追跡オプションは、次のカーネル Api を使用して割り当てられたメモリをサポートしています。

-   [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

-   [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)および i/o 要求パケット (IRP) データ構造を割り当てることができる他のルーチン

-   [**RtlAnsiStringToUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring)およびその他のランタイムライブラリ (RTL) 文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、プールの追跡を有効にすると、ドライバーの検証ツールは、アイドル状態のプロセスのコンテキストで、*クォータ*を持つカーネルプールメモリの割り当て試行を検出できます。 このような試行は、通常、ドライバーが DPC ルーチンからメモリを割り当てていることを意味します。 DPC ルーチンのスレッドまたはプロセスコンテキストは信頼性が低いため、そのプロセスに対するクォータの課金は正しくありません。

### <a name="span-idmonitoring_pool_trackingspanspan-idmonitoring_pool_trackingspanmonitoring-pool-tracking"></a><span id="monitoring_pool_tracking"></span><span id="MONITORING_POOL_TRACKING"></span>プール追跡の監視

メモリプールの割り当ての統計は、検証対象のドライバーごとに個別に監視できます。 これらの統計情報は、ドライバー検証マネージャー、検証ツールのコマンドライン、またはログファイルで表示できます。 詳細については、「[個々のカウンターの監視](monitoring-individual-counters.md)」をご覧ください。

カーネルデバッガー拡張 **! verifier 0x3**を使用すると、ドライバーがアンロードされた後に未処理のメモリ割り当てを検索したり、ドライバーの実行中に現在の割り当てを追跡したりできます。 この拡張機能には、プールタグ、プールのサイズ、各割り当てのアロケーターのアドレスも表示されます。 デバッガー拡張機能の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idpool_quota_charges_from_dpc_routinespanspan-idpool_quota_charges_from_dpc_routinespanspan-idpool_quota_charges_from_dpc_routinespanpool-quota-charges-from-dpc-routine"></a><span id="Pool_Quota_Charges_from_DPC_Routine"></span><span id="pool_quota_charges_from_dpc_routine"></span><span id="POOL_QUOTA_CHARGES_FROM_DPC_ROUTINE"></span>DPC ルーチンからのプールクォータの課金

カーネルドライバーは、 [**Exallocatepoolwithquotatag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)を呼び出して、カーネルプールのメモリを割り当て、現在のプロセスのプールクォータに割り当てられているバイト数を課金することができます。 通常、ドライバーは、アプリケーションからの要求に直接関連するメモリ割り当てのためにクォータを使用します。

遅延プロシージャ呼び出し (DPC) ルーチンは、任意のプロセスのコンテキストで実行できます。 そのため、DPC ルーチンからの課金クォータはランダムなプロセスになります。 さらに悪いことに、DPC ルーチンがアイドルプロセスのコンテキストで実行されていると、この状態が原因でメモリが破損したりシステムがクラッシュしたりする可能性があります。

Windows 7 以降では、ドライバーの検証ツールは DPC ルーチンからの[**Exallocatepoolwithquotの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)呼び出しを検出します。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーのプール追跡機能をアクティブ化できます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、プール追跡オプションは**ビット 3 (0x8)** で表されます。 プールの追跡を有効にするには、0x8 のフラグ値を使用するか、または0x8 をフラグ値に追加します。 例:

    ```
    verifier /flags 0x8 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動せずにプールの追跡をアクティブ化および非アクティブ化することもできます。 例:

    ```
    verifier /volatile /flags 0x8 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    プール追跡機能は、標準設定にも含まれています。 例:

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **プールの追跡**を選択 (チェック) します。

    プール追跡機能は、標準設定にも含まれています。 この機能を使用するには、ドライバー検証マネージャーで **[標準設定の作成]** をクリックします。

 

 





