---
title: 強制 IRQL チェック
description: 強制 IRQL チェック
ms.assetid: cb972a72-6504-4ed7-9618-2830192fda1d
keywords:
- 強制 IRQL チェック機能 WDK ドライバーの検証ツール
- IRQL 監視 WDK ドライバー検証ツール
- スピンロック WDK ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14005c3a40f14efc354dc8aaa093324e33971e76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839559"
---
# <a name="force-irql-checking"></a>強制 IRQL チェック


## <span id="ddk_forcing_irql_checking_tools"></span><span id="DDK_FORCING_IRQL_CHECKING_TOOLS"></span>


カーネルモードドライバーは、高い IRQL で、またはスピンロックを保持しながら、ページング可能なメモリにアクセスすることは禁止されていますが、このような操作は、ページが実際にはワーキングセットからトリミングされず、ディスクにページングされていない場合には認識されない可能性があります。

強制 IRQL チェックが有効になっている場合、ドライバーの検証ツールでは、システムメモリの使用に大きな負荷がかかっています。 検証対象のドライバーがスピンロックを要求したり、 **KeSynchronizeExecution**を呼び出したり、\_レベル以上をディスパッチする IRQL を発生させたりするたびに、すべてのシステムページング可能なプール、コード、およびデータ (ドライバーのページング可能なコードとデータを含む) が切り捨てられます。ワーキングセットから。 ドライバーがこのメモリのいずれかにアクセスしようとすると、ドライバーの検証ツールがバグチェックを発行します。

Windows Vista 以降では、このオプションを使用すると、特定の同期オブジェクトがページング可能なメモリに含まれているかどうかもドライバーの検証によって検出されます。 これらの同期オブジェクトは、オペレーティングシステムのカーネルが昇格された IRQL でアクセスしているため、ページングできません。 Driver Verifier は、ページング可能な[**Ktimer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)、prkmutex、pkspin\_LOCK、PRKEVENT、pkspin\_LOCK、PRKMUTEX、Peresource、 [**FAST\_MUTEX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を検出できます。

メモリ使用量に対するこの負荷は、検証用に選択されていないドライバーに直接は影響しません。 検証用に選択されていないドライバーで IRQL が発生しても、トリミング操作はトリガーされません。 ただし、検証対象のドライバーによって IRQL が発生した場合、ドライバーの検証ツールは、検証されていないドライバーが使用できるページをトリミングします。 このオプションがアクティブになっていると、検証されていないドライバーによってコミットされたエラーが発生することがあります。

### <a name="span-idmonitoring_irql_raises_and_spin_locksspanspan-idmonitoring_irql_raises_and_spin_locksspanmonitoring-irql-raises-and-spin-locks"></a><span id="monitoring_irql_raises_and_spin_locks"></span><span id="MONITORING_IRQL_RAISES_AND_SPIN_LOCKS"></span>IRQL の発生とスピンロックの監視

検証対象のドライバーによって行われた、IRQL の発生、スピンロック、および**KeSynchronizeExecution**の呼び出しの数を監視できます。 ドライバーの検証ツールによって、ワーキングセットからページング可能なメモリがトリミングされた回数も監視できます。 これらの統計情報は、ドライバー検証マネージャー、検証ツールのコマンドライン、またはログファイルで表示できます。 詳細については、「[グローバルカウンターの監視](monitoring-global-counters.md)」を参照してください。

カーネルデバッガー拡張機能の**検証ツール**を使用して、これらの統計情報を監視することもできます。 ドライバー検証ツールマネージャーと同様の情報が表示されます。 Windows XP 以降では、 **! verifier 0x8**拡張機能によって、検証されているドライバーによって行われた最近の IRQL の変更のログが表示されます。 デバッガー拡張機能の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespanspan-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespanspan-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespancalling-keentercriticalregion-or-keleavecriticalregion-at-dispatch_level-or-above"></a><span id="Calling_KeEnterCriticalRegion_or_KeLeaveCriticalRegion_at_DISPATCH_LEVEL_or_Above"></span><span id="calling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_above"></span><span id="CALLING_KEENTERCRITICALREGION_OR_KELEAVECRITICALREGION_AT_DISPATCH_LEVEL_OR_ABOVE"></span>ディスパッチ\_レベル以上での KeEnterCriticalRegion または KeLeaveCriticalRegion の呼び出し

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)と[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)は、通常のカーネル非同期プロシージャ呼び出し (apc) の配信で、ドライバーコードの重要なシーケンスの実行を同期するために使用できる api です。 **KeEnterCriticalRegion**および**KeLeaveCriticalRegion** api は、IRQL = DISPATCH\_レベル以上では呼び出せません。 ディスパッチ\_レベル以上で**KeEnterCriticalRegion**または**KeLeaveCriticalRegion**を呼び出すと、システムがハングしたり、メモリが破損したりする可能性があります。

Windows 7 以降では、Force IRQL チェックオプションが有効になっている場合、Driver Verifier はディスパッチ\_レベル以上でこれらの Api への呼び出しを検出します。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

Driver Verifier マネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーに対して強制 IRQL チェック機能を有効にすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、Force IRQL チェックオプションは**ビット 1 (0x2)** で表されます。 強制 IRQL チェックをアクティブにするには、フラグ値0x2 を使用するか、フラグ値に0x2 を追加します。 例:

    ```
    verifier /flags 0x2 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows 2000 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動せずに強制 IRQL チェックをアクティブ化および非アクティブ化することもできます。 例:

    ```
    verifier /volatile /flags 0x2 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    強制 IRQL チェック機能も、標準設定に含まれています。 例:

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **強制 IRQL チェック**を選択 (チェック) します。

    強制 IRQL チェック機能も、標準設定に含まれています。 この機能を使用するには、ドライバー検証マネージャーで **[標準設定の作成]** をクリックします。

 

 





