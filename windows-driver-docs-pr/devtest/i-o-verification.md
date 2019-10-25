---
title: I/o の検証
description: I/o の検証
ms.assetid: 41b77bba-fae8-453b-9872-911f5d5be3e6
keywords:
- I/o 検証機能 (WDK ドライバー検証ツール)
- レベル 1 i/o 検証 (WDK ドライバー検証ツール)
- レベル2の i/o 検証 WDK ドライバーの検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c2be91a6bf7197dd306a3c729efe359744463f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840264"
---
# <a name="io-verification"></a>I/o の検証


## <span id="ddk_i_o_verification_tools"></span><span id="DDK_I_O_VERIFICATION_TOOLS"></span>


Driver Verifier には、次の2つのレベルの i/o 検証があります。

-   I/o 検証が選択されている場合は常に、*レベル1の I/o 検証*が常にアクティブになります。

-   Windows XP 以降で i/o 検証が選択されている場合は常に、*レベル2の I/o 検証*が常にアクティブになります。 Windows 2000 では、両方のレベルを含めるように i/o の検証を構成することも、レベル1のテストだけを構成することもできます。

**関連項目:** windows 7 以降のバージョンの windows オペレーティングシステムでの強化された i/o[検証](enhanced-i-o-verification.md)、i/o 検証を選択した場合は、拡張 i/o 検証が自動的にアクティブ化されます。 別のオプションとして選択することはできません。

### <a name="span-idlevel_1_i_o_verificationspanspan-idlevel_1_i_o_verificationspanlevel-1-io-verification"></a><span id="level_1_i_o_verification"></span><span id="LEVEL_1_I_O_VERIFICATION"></span>レベル1の i/o 検証

レベル1の i/o 検証が有効になっている場合、 **Ioallocateirp**で取得したすべての irp が特別なプールから割り当てられ、その使用が追跡されます。

また、ドライバーの検証ツールは、次のような無効な i/o 呼び出しを確認します。

-   型が IO でない IRP の解放を試みます\_型\_IRP

-   無効なデバイスオブジェクトを**IoCallDriver**に渡します。

-   無効な状態を含んでいるか、まだキャンセルルーチンが設定されている**IoCompleteRequest**への IRP の引き渡し

-   ドライバーディスパッチルーチンの呼び出しにおける IRQL の変更

-   スレッドに関連付けられたままになっている IRP の解放を試みます。

-   初期化されたタイマーが既に含まれている**Ioinitializetimer**にデバイスオブジェクトを渡します。

-   無効なバッファーを**IoBuildAsynchronousFsdRequest**または**IoBuildDeviceIoControlRequest**に渡します。

-   I/o 状態ブロックを IRP に渡すと、この i/o ステータスブロックが、過剰にアンワインドしているスタックに割り当てられます。

-   イベントオブジェクトを IRP に渡します。このイベントオブジェクトは、アンワインドが大きすぎるスタックに割り当てられます。

特殊な IRP プールのサイズは限られているため、i/o の検証は、一度に1つのドライバーでのみ使用される場合に最も効果的です。

I/o 検証レベル1のエラーにより、バグチェック0xC9 が発行されます。 このバグチェックの最初のパラメーターは、どのような違反が発生したかを示します。 完全なパラメーターの一覧については、「[**バグチェック 0xC9**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation) (DRIVER\_VERIFIER\_iomanager\_違反)」を参照してください。

### <a name="span-idlevel_2_i_o_verificationspanspan-idlevel_2_i_o_verificationspanlevel-2-io-verification"></a><span id="level_2_i_o_verification"></span><span id="LEVEL_2_I_O_VERIFICATION"></span>レベル2の i/o 検証

I/o 検証レベル2のエラーは、ブルースクリーン、クラッシュダンプファイル、およびカーネルデバッガーで、さまざまな方法で表示されます。

ブルースクリーンでは、これらのエラーはメッセージ**IO システムの検証エラー**と文字列 **WDM ドライバーエラー * * * XXX*で示されます。 *xxx*は i/o エラーコードです。

クラッシュダンプファイルでは、これらのエラーのほとんどは、i/o エラーコードと共に、メッセージの**バグチェック 0xC9 (DRIVER\_VERIFIER\_IOMANAGER\_違反)** によって示されます。 この場合、i/o エラーコードはバグチェック0xC9 の最初のパラメーターとして表示されます。 残りの部分は、ドライバーの検証ツールのエラーコードと共に、**バグチェック 0xC4 (driver\_VERIFIER\_検出された\_違反)** によって示されます。 この場合、ドライバーの検証ツールのエラーコードは、バグチェック0xC4 の最初のパラメーターとして表示されます。

カーネルデバッガー (KD または WinDbg) では、これらのエラーは、メッセージ「 **WDM ドライバーエラー** 」と説明のテキスト文字列によって示されます。 カーネルデバッガーがアクティブになっている場合、レベル2のエラーを無視し、システムの操作を再開することができます。 (これは他のバグチェックではできません)。

青色の画面、クラッシュダンプファイル、およびカーネルデバッガーは、それぞれ追加情報も表示します。 ほとんどの i/o 検証レベル2のエラーメッセージの詳細については、「[**バグチェック 0xC9**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)」を参照してください。 その他の詳細については、「[**バグチェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)」を参照してください。

Windows Vista 以降では、i/o 検証オプションによって次のドライバーエラーがチェックされます。

-   ユーザーモードのアプリケーションで発生した Irp の完了と取り消しに時間がかかりすぎています。

-   まだ取得されていない削除ロックを解放しています。

-   対応する[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)呼び出しで使用されるタグパラメーターとは異なるタグパラメーターを指定して、 [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)または[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出しています。

-   割り込みが無効になっている[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出しています。

-   ディスパッチ\_レベルより大きい IRQL で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出しています。

-   割り込みが無効になっているドライバーディスパッチルーチンからを返します。

-   ドライバーディスパッチルーチンから、変更された IRQL を返します。

-   Apc が無効になっているドライバーディスパッチルーチンからを返します。 この場合、ドライバーは[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)よりも多くの[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出している可能性があります。これは、[**バグチェック 0x20**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x20--kernel-apc-pending-during-exit) (カーネル\_APC\_保留中の\_\_終了中) の主な原因です。[**バグチェック 0x1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x1--apc-index-mismatch) (APC\_インデックス\_不一致)。

Windows 7 以降では、i/o 検証オプションによって次のドライバーエラーがチェックされます。

-   [**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出して、irp の解放を試みます。 Irp は、 [**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を使用して解放する必要があります。

さらに、このオプションを使用して、別の一般的なドライバーバグを検出し、削除ロックを再初期化することもできます。 削除ロックデータ構造は、デバイス拡張機能内に割り当てる必要があります。 これにより、i/o マネージャーは、デバイスオブジェクトが削除された場合にのみ\_ロック構造を削除\_、IO を保持するメモリを解放します。 ドライバーが次の3つの手順を実行する場合は、手順 2. の後に、アプリケーションまたはドライバーが Device1 への参照を保持している可能性があります。

-   Device1 に対応する\_ロック構造を削除\_IO を割り当てますが、Device1's extension の外に割り当てを行います。
-   Device1 が削除されるときに[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出します。
-   同じロックに対して[**Ioデバイス 2 Eremovelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)を呼び出して、これをの削除ロックとして再利用します。

手順2の後に、アプリケーションまたはドライバーが Device1 への参照を保持している可能性があります。 このデバイスが削除された場合でも、アプリケーションまたはドライバーは引き続き Device1 に要求を送信できます。 そのため、i/o マネージャーによって Device1 が削除されるまで、新しい削除ロックと同じメモリを再利用するのは安全ではありません。 別のスレッドが取得しようとしているときに同じロックを再初期化すると、ロックが破損し、ドライバーとシステム全体に対して予期しない結果が発生する可能性があります。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、i/o 検証を選択すると、[拡張 I/o 検証](enhanced-i-o-verification.md)が自動的にアクティブ化されます。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの i/o 検証機能をアクティブ化できます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインを実行します。**

    コマンドラインでは、i/o 検証オプションは**ビット 4 (0x10)** で表されます。 I/o の検証をアクティブにするには、フラグ値に0x10 を使用するか、フラグ値に0x10 を追加します。 例:

    ```
    verifier /flags 0x10 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows 2000 では、 **/iolevel**パラメーターを使用して、レベル 1 (既定値) またはレベル1とレベル2の両方をアクティブにすることができます。 Windows の新しいバージョンでは、i/o 検証をアクティブ化すると、レベル1とレベル2の両方が常にアクティブ化されます。

    たとえば、次のコマンドは、Windows 2000 を実行しているコンピューターでレベル1とレベル2の i/o 検証をアクティブにします。

    ```
    verifier /flags 0x10 /iolevel 2 /driver MyDriver.sys
    ```

    Windows Vista 以降のバージョンの Windows では、コマンドに **/volatile**パラメーターを追加することで、コンピューターを再起動せずに I/o の検証をアクティブ化および非アクティブ化することもできます。 例:

    ```
    verifier /volatile /flags 0x10 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    I/o 検証機能は、標準設定にも含まれています。 例:

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    2.  [**完全な一覧から個々の設定を選択]** を選択します。
    3.  **[I/o の確認]** を選択します。

    I/o 検証機能は、標準設定にも含まれています。 この機能を使用するには、ドライバー検証マネージャーで **[標準設定の作成]** をクリックします。

 

 





