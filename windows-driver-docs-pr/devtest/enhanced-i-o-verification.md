---
title: 強化された i/o 検証
description: 強化された i/o 検証
ms.assetid: ce8a0b22-fa27-45e5-b013-b3accf604ed4
keywords:
- 拡張 i/o 検証機能 (WDK Driver Verifier)
- I/o 検証機能 (WDK ドライバー検証ツール)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e6f1a4a8b2ec82ab8536fd5130f785c3a12a51f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840268"
---
# <a name="enhanced-io-verification"></a>強化された i/o 検証


この機能は、windows XP 以降のバージョンの Windows オペレーティングシステムでのみ使用できます。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、i/o 検証を選択すると、拡張 i/o 検証が自動的にアクティブ化されます。 別のオプションとして選択することはできません。

拡張 i/o 検証がアクティブになると、ドライバー検証ツールは、複数の i/o マネージャールーチンの呼び出しを監視し、PnP Irp、電力 Irp、および WMI Irp のストレステストを実行します。

Windows Vista および Windows XP では、拡張 i/o 検証は[I/o 検証](i-o-verification.md)とは無関係にアクティブ化されますが、両方のオプションを選択すると、ドライバー内の i/o インターフェイスメソッドの完全なテストを行うことができます。

### <a name="span-idfeatures_of_enhanced_i_o_verificationspanspan-idfeatures_of_enhanced_i_o_verificationspanfeatures-of-enhanced-io-verification"></a><span id="features_of_enhanced_i_o_verification"></span><span id="FEATURES_OF_ENHANCED_I_O_VERIFICATION"></span>強化された i/o 検証の機能

ドライバーの検証機能では、強化された i/o 検証をアクティブ化すると、次のチェックが追加されます。

-   すべての Irp を監視し、ドライバーが[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出した場合にのみ、ステータス\_保留中であることを確認します。

-   [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)の使用を監視して、ドライバーが同じデバイスを削除していないことを確認します。これにより、デバイスオブジェクトの不適切なデタッチと削除が検出されます。

-   ドライバーがすべての[**Ioskipに**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)対して、すべての iolocation 呼び出しを正しくアンワインドしたことを確認します。

新しいストレスとテストには次のようなものがあります。

-   列挙されたデバイスの順序をスクランブルして、プラグアンドプレイ (PnP) ドライバーがデバイスの開始位置を想定していないことを確認します。

-   PnP と電源 Irp の完了時の状態を調整し、ディスパッチルーチンから間違った状態を返すドライバーをキャッチします。

-   ドライバーコードパスのバグをテストするための偽の電源 Irp を送信する。

-   偽の WMI Irp を送信して、ドライバーコードパスのバグをテストします。

-   すべての WDM スタックにフェイクフィルターを挿入します。

### <a name="span-iddisplaying_enhanced_i_o_verification_errorsspanspan-iddisplaying_enhanced_i_o_verification_errorsspandisplaying-enhanced-io-verification-errors"></a><span id="displaying_enhanced_i_o_verification_errors"></span><span id="DISPLAYING_ENHANCED_I_O_VERIFICATION_ERRORS"></span>強化された i/o 検証エラーの表示

拡張 i/o 検証によって検出されたドライバーエラーは、[レベル2の I/o 検証](i-o-verification.md)でキャッチされたものと同じ方法で表示されます。

ブルースクリーンでは、これらのエラーはメッセージ**IO システムの検証エラー**と文字列**WDM ドライバーエラー** *xxx*によって示されます。ここで、 *xxx*は i/o エラーコードです。

クラッシュダンプファイルでは、これらのエラーは、i/o エラーコードと共に、メッセージの**バグチェック 0xC9 (DRIVER\_VERIFIER\_IOMANAGER\_違反)** によって記録されます。 この場合、i/o エラーコードはバグチェック0xC9 の最初のパラメーターとして表示されます。

カーネルデバッガー (KD または WinDbg) では、これらのエラーは、メッセージ「 **WDM ドライバーエラー** 」と説明のテキスト文字列によって示されます。 カーネルデバッガーがアクティブになっている場合、レベル2のエラーを無視し、システムの操作を再開することができます。 (これは他のバグチェックではできません)。

青色の画面、クラッシュダンプファイル、およびカーネルデバッガーは、それぞれ追加情報も表示します。 すべての i/o 検証レベル2のエラーメッセージの詳細については、「 [**Bug Check 0xC9**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)」を参照してください。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの強化された i/o 検証機能をアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

**注**  windows 7 以降のバージョンの windows オペレーティングシステムでは、 [i/o](i-o-verification.md)検証を選択すると、拡張 i/o 検証が自動的にアクティブ化されます。 別のオプションとして選択することはできません。

 

-   **コマンドラインで**

    コマンドラインでは、拡張 i/o 検証オプションは**ビット 6 (0x40)** で表されます。 拡張 i/o 検証をアクティブ化するには、フラグ値0x40 を使用するか、フラグ値に0x40 を追加します。 例:

    ```
    verifier /flags 0x40 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、コマンドに **/volatile**パラメーターを追加することによって、コンピューターを再起動せずに拡張 i/o 検証をアクティブ化および非アクティブ化することもできます。 例:

    ```
    verifier /volatile /flags 0x40 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[拡張 i/o の確認]** を選択します。

    DMA 検証機能は、標準設定にも含まれています。 この機能を使用するには、ドライバー検証マネージャーで **[標準設定の作成]** をクリックします。

 

 





