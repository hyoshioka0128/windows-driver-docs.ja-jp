---
title: 強制 IRQL 検査
description: 強制 IRQL 検査
ms.assetid: cb972a72-6504-4ed7-9618-2830192fda1d
keywords:
- 強制 IRQL 検査機能 WDK Driver Verifier
- IRQL WDK Driver Verifier の監視
- スピン ロック WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73b01d0459207857b8a573334ad4d79eb7857e9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536072"
---
# <a name="force-irql-checking"></a>強制 IRQL 検査


## <span id="ddk_forcing_irql_checking_tools"></span><span id="DDK_FORCING_IRQL_CHECKING_TOOLS"></span>


カーネル モード ドライバーが高 IRQL でまたはスピン ロックを保持しているときに、ページング可能なメモリへのアクセスを禁止されていますが、このようなアクションは可能性があります、作業が設定され、ディスクにページ アウト ページが実際にからトリミングされた場合は認識されません。

強制 IRQL 検査を有効にすると、Driver Verifier は、システム メモリの使用方法の大きなプレッシャーを提供します。 検証されているドライバーでは、スピン ロックを要求するたびに呼び出す**KeSynchronizeExecution**、ディスパッチする指示または\_レベル、または以降では、すべてのシステムのページング可能なプール、コード、および (を含む、ドライバーのデータワーキング セットからは、ページング可能なコードとデータ) は切り捨てられます。 ドライバーでは、このメモリのいずれかにアクセスしようとして、Driver Verifier はバグ チェックを発行します。

Windows Vista 以降、このオプションによってページング可能なメモリ内で特定の同期オブジェクトが含まれている場合を検出するために、ドライバーの検証ツールです。 これらの同期オブジェクトは、オペレーティング システムのカーネルが管理者特権での IRQL でアクセスがあるためにページングされることはできません。 Driver Verifier は、ページング可能な検出できる[ **KTIMER**](https://msdn.microsoft.com/library/windows/hardware/ff554250)、PRKMUTEX、PKSPIN\_ロック、PRKEVENT、PKSPIN\_ロック、PRKSEMAPHORE、PERESOURCE、および[ **高速\_ミュー テックス**](https://msdn.microsoft.com/library/windows/hardware/ff545715)構造体。

メモリ使用量には、この負荷では、検証のために選択されていないドライバーは直接影響はありません。 検証のために選択されていないドライバーの IRQL が発生したときに、トリミング アクションは発生しません。 ただし、ドライバーは検証されているのでは、IRQL が発生したときにドライバーの検証ツールが検証されないドライバーで使用できるページをトリミングします。 これが検証されないドライバーによってコミットされたエラーは、このオプションがアクティブなときに場合によってはキャッチ可能性があります。

### <a name="span-idmonitoringirqlraisesandspinlocksspanspan-idmonitoringirqlraisesandspinlocksspanmonitoring-irql-raises-and-spin-locks"></a><span id="monitoring_irql_raises_and_spin_locks"></span><span id="MONITORING_IRQL_RAISES_AND_SPIN_LOCKS"></span>監視の IRQL が発生し、スピン ロック

IRQL 発生させ、スピン ロック、およびへの呼び出しの数**KeSynchronizeExecution**によるドライバーが監視されていることを確認できます。 Driver Verifier がワーキング セットからページング可能なメモリがトリムされる回数も監視できます。 ドライバー検証ツール マネージャーによって、Verifier.exe コマンドライン、またはログ ファイルで、これらの統計情報を表示できます。 参照してください[グローバル カウンターの監視](monitoring-global-counters.md)詳細についてはします。

カーネル デバッガー拡張機能 **! verifier**これらの統計情報を監視するも使用することができます。 ドライバー検証マネージャーのする同様の情報が表示されます。 Windows XP 以降では、 **! verifier 0x8**拡張機能が検証されているドライバーによって行われた最近の IRQL 変更のログに表示されます。 デバッガーの拡張機能については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

### <a name="span-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespanspan-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespanspan-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespancalling-keentercriticalregion-or-keleavecriticalregion-at-dispatchlevel-or-above"></a><span id="Calling_KeEnterCriticalRegion_or_KeLeaveCriticalRegion_at_DISPATCH_LEVEL_or_Above"></span><span id="calling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_above"></span><span id="CALLING_KEENTERCRITICALREGION_OR_KELEAVECRITICALREGION_AT_DISPATCH_LEVEL_OR_ABOVE"></span>ディスパッチで KeEnterCriticalRegion または KeLeaveCriticalRegion を呼び出す\_レベル以上

[**KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)と[ **KeLeaveCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552964)することができる Api 使用配信とドライバーのコードの重要なシーケンスの実行を同期するには通常カーネルの非同期プロシージャは、(Apc) を呼び出します。 **KeEnterCriticalRegion**と**KeLeaveCriticalRegion** IRQL で Api を呼び出すことができません = ディスパッチ\_レベルまたはそれ以降。 呼び出す**KeEnterCriticalRegion**または**KeLeaveCriticalRegion**ディスパッチで\_レベルまたはシステム ハングまたはメモリ破損が発生できる以降。

Windows 7 以降、Driver Verifier 検出ディスパッチでこれらの Api の呼び出しを\_レベル、または場合強制 IRQL 検査オプションを有効にします。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの強制 IRQL 検査機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    、コマンドラインでは、強制 IRQL 検査オプションで表される**ビット 1 (0x2)** します。 強制 IRQL 検査を有効にするには、0x2 のフラグの値を使用して、または 0x2 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x2 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows 2000 と Windows の以降のバージョンでもアクティブ化し、追加することで、コンピューターを再起動しなくても強制 IRQL 検査を非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x2 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    強制 IRQL 検査機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)**強制 IRQL 検査**します。

    強制 IRQL 検査機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





