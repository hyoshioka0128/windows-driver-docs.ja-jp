---
title: プールの追跡
description: プールの追跡では、ドライバーによって行われるメモリ割り当てを監視します。
ms.assetid: 5b8aa775-d908-4a7a-b54f-6c63ac1ebd13
keywords:
- メモリ プールの追跡機能 WDK Driver Verifier
- プールの追跡機能の WDK Driver Verifier
- WDK の Driver Verifier のメモリ割り当て
- WDK の Driver Verifier のメモリ リークします。
- WDK の Driver Verifier の未解放のメモリ割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8562a9c8ebbc6523376b0c5e64df317b19c8c1e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536793"
---
# <a name="pool-tracking"></a>プールの追跡


プールの追跡では、ドライバーによって行われるメモリ割り当てを監視します。 ドライバーが読み込まれている時に、Driver Verifier は、ドライバーによって行われたすべての割り当てが解放されたことによりします。

## <span id="ddk_memory_pool_tracking_tools"></span><span id="DDK_MEMORY_POOL_TRACKING_TOOLS"></span>


未解放のメモリ割り当て (とも呼ばれる*メモリ リーク*) は短くしたオペレーティング システムのパフォーマンスの一般的な原因です。 これらはシステム プールのフラグメントあり、最終的にシステムのクラッシュの原因します。

このオプションがアクティブな場合 (パラメーター 1 と等しい数 0x62) の場合は、すべての割り当てを解放せず、ドライバーをアンロード Driver Verifier に 0xC4 のバグ チェックが発行されます。

Driver Verifier では、パラメーター 1 0x51、0x52、0x53、0x54、または 0x59 このバグ チェックが発行した場合、ドライバーがその割り当て外にメモリに書き込まれます。 この場合は、有効にしてください、[特別なプール](special-pool.md)エラーのソースを検索する機能。

参照してください[**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)、バグの一覧については、パラメーターを確認します。

以降 Windows Vista では、ロックされたページの追跡もにより、プールの追跡オプションを有効にします。 このオプションがアクティブな場合は、Driver Verifier は発行[**バグ チェック 0xCB** ](https://msdn.microsoft.com/library/windows/hardware/ff560212) (ドライバー\_左\_ロック\_ページ\_IN\_プロセス) を解放するドライバーが失敗した場合は、I/O 操作の後にページをロックします。

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、プールの追跡オプションは、次のカーネル Api を使用して割り当てられたメモリをサポートしています。

-   [**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)

-   [**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)と I/O を割り当てることができるその他のルーチン要求パケット (IRP) データ構造体

-   [**RtlAnsiStringToUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561729)およびその他のランタイム ライブラリ (RTL) の文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、プールの追跡を有効にすると、Driver Verifier を検出できますでカーネル プールのメモリを割り当てようとする*クォータ*アイドル状態のプロセスのコンテキストでします。 このような試行は通常、DPC ルーチンから、ドライバーは、メモリを意味します。 DPC ルーチンのスレッドまたはプロセスのコンテキストは、そのプロセスのクォータを請求しようとしていますが正しくないために、信頼性が高くです。

### <a name="span-idmonitoringpooltrackingspanspan-idmonitoringpooltrackingspanmonitoring-pool-tracking"></a><span id="monitoring_pool_tracking"></span><span id="MONITORING_POOL_TRACKING"></span>プールの追跡の監視

メモリ プールの割り当ての統計情報は、検証されているドライバーごとに個別に監視できます。 ドライバー検証ツール マネージャーによって、Verifier.exe コマンドライン、またはログ ファイルで、これらの統計情報を表示できます。 参照してください[カウンターを個別に監視](monitoring-individual-counters.md)詳細についてはします。

カーネル デバッガー拡張機能 **! verifier 0x3**ドライバーが読み込まれるまたはドライバーの中に現在の割り当てを追跡するために実行した後は、未処理のメモリ割り当てを検索するために使用できます。 この拡張機能は、プール タグ、プールのサイズと、各割り当てのアロケーターのアドレスにも表示されます。 デバッガーの拡張機能については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

### <a name="span-idpoolquotachargesfromdpcroutinespanspan-idpoolquotachargesfromdpcroutinespanspan-idpoolquotachargesfromdpcroutinespanpool-quota-charges-from-dpc-routine"></a><span id="Pool_Quota_Charges_from_DPC_Routine"></span><span id="pool_quota_charges_from_dpc_routine"></span><span id="POOL_QUOTA_CHARGES_FROM_DPC_ROUTINE"></span>DPC ルーチンからプール クォータの料金

カーネル ドライバーを呼び出すことができます[ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513)カーネル プールのメモリを割り当てるし、現在のプロセスのプール クォータに割り当てられているバイト数を請求します。 通常、ドライバーは、アプリケーションから受信した要求に直接関連するメモリ割り当てのクォータを使用します。

遅延プロシージャ呼び出し (DPC) のルーチンは、任意のプロセスのコンテキストで実行できます。 そのため、充電 DPC ルーチンからのクォータには、ランダムなプロセスが請求されます。 さらに悪い、DPC ルーチンがアイドル状態のプロセスのコンテキストで実行するとこの条件によりメモリの破損またはシステムがクラッシュします。

Windows 7 以降、Driver Verifier を検出した[ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513) DPC ルーチンからの呼び出し。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバー プールの追跡機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    によって表されるプールの追跡オプションをコマンドラインで**ビット 3 (0x8)** します。 プールの追跡を有効にするには、0x8 のフラグの値を使用して、または 0x8 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x8 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows Vista および Windows の以降のバージョンをアクティブ化し、プールの追跡を非アクティブ化を追加して、コンピューターを再起動しなくても、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x8 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    プールの追跡機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)**プール追跡**します。

    プールの追跡機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





