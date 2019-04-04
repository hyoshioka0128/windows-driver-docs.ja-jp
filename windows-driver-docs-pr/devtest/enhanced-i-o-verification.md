---
title: 強化された I/O の検証
description: 強化された I/O の検証
ms.assetid: ce8a0b22-fa27-45e5-b013-b3accf604ed4
keywords:
- 強化された I/O の検証機能 WDK Driver Verifier
- I/O の検証機能 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2edd9c7ed87e3e9a029c44ae335b02e116d90c80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532210"
---
# <a name="enhanced-io-verification"></a>強化された I/O の検証


この機能は Windows XP および Windows オペレーティング システムの以降のバージョンで使用できるだけです。

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、I/O の検証の強化は I/O の検証を選択すると、自動的にアクティブ化されます。 それが利用できないか個別のオプションとして選択するために必要です。

強化された I/O の検証がアクティブになるドライバーの検証ツールはいくつかの I/O マネージャー ルーチンの呼び出しを監視し、PnP Irp、電源 Irp および WMI の Irp のストレスのテストを実行します。

Windows Vista および Windows XP では、I/O の検証の強化がアクティブになるとは無関係に[I/O の検証](i-o-verification.md)が両方のオプションを選択すると、ドライバーの I/O インターフェイスのメソッドのより完全なテストを提供します。

### <a name="span-idfeaturesofenhancedioverificationspanspan-idfeaturesofenhancedioverificationspanfeatures-of-enhanced-io-verification"></a><span id="features_of_enhanced_i_o_verification"></span><span id="FEATURES_OF_ENHANCED_I_O_VERIFICATION"></span>強化された I/O の検証の機能

Driver Verifier は、強化された I/O の検証を有効にすると、次のチェックを追加します。

-   監視、ドライバーが状態を返すことを確認するためのすべての Irp\_PENDING 呼び出した場合にのみ[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

-   使用を監視[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)と不適切なデタッチしたり、デバイス オブジェクトの削除を検出すること、ドライバーがないデバイスを削除する同じ 2 回以上のことを確認します。

-   あるドライバー正しくアンワインドすべてを確認します。 [ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)呼び出し。

新しい負荷とテストは、次のとおりです。

-   スクランブルの順序と、プラグ アンド プレイ (PnP) ドライバーが起動順序、デバイスに関する前提条件を作成しないことを確認して、デバイスが列挙されます。

-   ドライバーがディスパッチ ルーチンから正しくない状態を返すことを検出、完了したときに、PnP の状態と電源 Irp を調整することです。

-   ドライバーのコード パスのバグをテストする偽 Power Irp を送信します。

-   ドライバーのコード パスのバグをテストする偽の WMI Irp を送信します。

-   偽のフィルターをすべて WDM スタックに挿入します。

### <a name="span-iddisplayingenhancedioverificationerrorsspanspan-iddisplayingenhancedioverificationerrorsspandisplaying-enhanced-io-verification-errors"></a><span id="displaying_enhanced_i_o_verification_errors"></span><span id="DISPLAYING_ENHANCED_I_O_VERIFICATION_ERRORS"></span>強化された I/O の検証エラーを表示します。

I/O の検証の強化によってキャッチ ドライバー エラーによってキャッチものと同じように表示されます[レベル 2 の I/O の検証](i-o-verification.md)です。

青の画面では、これらのエラーは、メッセージによって記録されます**IO システム検証エラー**と文字列**WDM ドライバー エラー** *XXX*ここで、 *XXX*I/O エラー コードします。

メッセージによって、クラッシュ ダンプ ファイルにこれらのエラーが記録されます**バグチェック 0xC9 (ドライバー\_VERIFIER\_IOMANAGER\_違反)**、I/O エラー コードと共にします。 この場合、I/O エラー コードは、0xC9 のバグ チェックの最初のパラメーターとして表示されます。

カーネル デバッガー (KD または WinDbg) でこれらのエラーは、メッセージによって記録されます**WDM ドライバー エラー**と説明のテキスト文字列。 カーネル デバッガーがアクティブな場合は、レベル 2 のエラーを無視し、システムの操作を再開することです。 (これが、その他のバグ チェックで可能です)

ブルー スクリーン、クラッシュ ダンプ ファイル、およびカーネル デバッガーの各追加情報を表示もできます。 すべての I/O の検証レベル 2 のエラー メッセージの詳細については、[**バグ チェック 0xC9**](https://msdn.microsoft.com/library/windows/hardware/ff560205)を参照してください。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバの I/O の検証の強化された機能をアクティブにできます。 詳細については、[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)を参照してください。

**注**  Windows 7 および Windows オペレーティング システムの以降のバージョンでは、強化された I/O の検証は自動的にアクティブ化を選択すると[I/O の検証](i-o-verification.md)です。 それが利用できないか個別のオプションとして選択するために必要です。

 

-   **コマンドラインで**

    、コマンドラインでは、強化された I/O の検証オプションで表される**ビット 6 (0x40)** します。 強化された I/O の検証を有効にするには、0x40 のフラグの値を使用して、または 0x40 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x40 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンもアクティブ化し、I/O の検証の強化を追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x40 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、[揮発性の設定を使用する](using-volatile-settings.md)を参照してください。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)**強化された I/O の検証**です。

    DMA の検証機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





