---
title: I/O の検証
description: I/O の検証
ms.assetid: 41b77bba-fae8-453b-9872-911f5d5be3e6
keywords:
- I/O の検証機能 WDK Driver Verifier
- レベル 1 I/O 検証 WDK Driver Verifier
- レベル 2 I/O 検証 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4235a98c84aade321da760c374e6d1985e5ba49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358265"
---
# <a name="io-verification"></a>I/O の検証


## <span id="ddk_i_o_verification_tools"></span><span id="DDK_I_O_VERIFICATION_TOOLS"></span>


Driver Verifier では、I/O の検証の 2 つのレベルがあります。

-   *レベル 1 の I/O の検証*I/O の検証が選択されるたびにアクティブでは常にします。

-   *第 2 レベルの I/O の検証*は I/O の検証には、Windows XP 以降が選択されているときに常にアクティブです。 Windows 2000 では、I/O の検証は、両方のレベルを含めるように構成できますか、レベル 1 だけをテストします。

**参照してください。** [I/O の検証の強化](enhanced-i-o-verification.md)Windows 7 および Windows オペレーティング システムの以降のバージョンでは、強化された I/O の検証は自動的にアクティブ化 I/O の検証を選択するとします。 それが利用できないか個別のオプションとして選択するために必要です。

### <a name="span-idlevel_1_i_o_verificationspanspan-idlevel_1_i_o_verificationspanlevel-1-io-verification"></a><span id="level_1_i_o_verification"></span><span id="LEVEL_1_I_O_VERIFICATION"></span>第 1 レベルの I/O の検証

レベル 1 の I/O の検証を有効にすると、すべての Irp 経由で取得した**IoAllocateIrp**は特別なプールから割り当てられ、その使用を追跡します。

さらに、Driver Verifier を I/O 呼び出しの無効な (など) を確認します。

-   型でない IO IRP の解放を試みます\_型\_IRP

-   パスに無効なデバイス オブジェクトの**保留**

-   パスに IRP の**IoCompleteRequest**無効な状態を格納しているか、キャンセルの日常的なセットをまだ

-   ドライバーのディスパッチ ルーチンへの呼び出しの間での IRQL への変更

-   関連付けられたスレッドは IRP を解放しようとしています。

-   デバイス オブジェクトのパスを**IoInitializeTimer**を既に初期化済みのタイマーが含まれています

-   パスに無効なバッファーの**IoBuildAsynchronousFsdRequest**または**IoBuildDeviceIoControlRequest**

-   この状態の I/O ブロックが離れすぎてアンワインドがスタックに割り当てられるときに、IRP を I/O 状態ブロックのパス

-   このイベント オブジェクトが離れすぎてアンワインドがスタックに割り当てられるときに、IRP にイベント オブジェクトのパス

特別なプールの IRP では、サイズの制限であるため、一度に 1 つのドライバーの使用のみ I/O の検証は最も効果的なです。

検証レベル 1 の I/O エラーが発生するバグ チェック 0xC9 が発行されます。 このバグ チェックの最初のパラメーターでは、どのような違反が発生したことを示します。 参照してください[**バグ チェック 0xC9** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation) (ドライバー\_VERIFIER\_IOMANAGER\_違反) 完全なパラメーターの一覧についてはします。

### <a name="span-idlevel_2_i_o_verificationspanspan-idlevel_2_i_o_verificationspanlevel-2-io-verification"></a><span id="level_2_i_o_verification"></span><span id="LEVEL_2_I_O_VERIFICATION"></span>第 2 レベルの I/O の検証

さまざまな方法で検証レベル 2 の I/O エラーが表示されます。 カーネル デバッガーにし、クラッシュ ダンプ ファイルには、ブルー スクリーンにします。

青の画面では、これらのエラーは、メッセージによって記録されます**IO システム検証エラー**と文字列 **WDM ドライバー エラー * * * XXX*ここで、 *XXX* I/O エラー コードします。

メッセージによってクラッシュ ダンプ ファイルでは、ほとんどのエラーが示されて**バグチェック 0xC9 (ドライバー\_VERIFIER\_IOMANAGER\_違反)** 、I/O エラー コードと共にします。 この場合、I/O エラー コードは、0xC9 のバグ チェックの最初のパラメーターとして表示されます。 残りの部分は、メッセージによって記録されます**0xC4 のバグ チェック (ドライバー\_VERIFIER\_検出\_違反)** 、Driver Verifier のエラー コードと共にします。 この場合は、Driver Verifier のエラー コードは、バグ チェック 0xC4 の最初のパラメーターとして表示されます。

カーネル デバッガー (KD または WinDbg) でこれらのエラーは、メッセージによって記録されます**WDM ドライバー エラー**と説明のテキスト文字列。 カーネル デバッガーがアクティブな場合は、レベル 2 のエラーを無視し、システムの操作を再開することです。 (これが、その他のバグ チェックで可能です)

ブルー スクリーン、クラッシュ ダンプ ファイル、およびカーネル デバッガーの各追加情報を表示もできます。 ほとんどの I/O の検証レベル 2 のエラー メッセージの詳細については、次を参照してください。 [**バグ チェック 0xC9**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)します。 残りの部分は、次を参照してください。 [**バグ チェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)します。

次のドライバー エラー以降 Window Vista では、I/O の検証オプションを確認します。

-   完了し、ユーザー モード アプリケーションから発信された Irp のキャンセルに長時間かかっています。

-   まだ取得されていないを削除ロックを解除します。

-   呼び出す[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)または[ **IoReleaseRemoveLockAndWait** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)タグ パラメーターとは異なるタグ パラメーター対応するために使用[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)呼び出します。

-   呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)に割り込みを無効になっています。

-   呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)ディスパッチより大きい IRQL で\_レベル。

-   割り込みを無効になっているドライバーのディスパッチ ルーチンから返します。

-   変更された IRQL とドライバーのディスパッチ ルーチンから返すことです。

-   Apc を無効になっているのでドライバーのディスパッチ ルーチンから返します。 この場合、ドライバーを呼び出したことがある[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)回よりも[ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)、これは、主な原因[**バグ チェック 0x20** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x20--kernel-apc-pending-during-exit) (カーネル\_APC\_PENDING\_に\_終了) と[ **バグ チェック 0x1** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x1--apc-index-mismatch) (APC\_インデックス\_が一致しません)。

次のドライバー エラーの Windows 7 以降、I/O の検証オプションを確認します。

-   Irp を呼び出すことによって解放しようとしています。 [ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)します。 Irp を使用して解放する必要があります[ **IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)します。

さらに、もう 1 つの一般的なドライバーのバグを検出するためにこのオプションを使用できます: ロックを削除して再初期化します。 デバイスの拡張機能の内部データ構造を割り当てる必要があるロックを削除します。 これにより、I/O マネージャーが、IO を保持するメモリを解放する\_削除\_デバイス オブジェクトが削除された場合にのみ、ロック構造体。 ドライバーは、次の 3 つの手順を実行する場合、手順 2 の後にアプリケーションやドライバーも保持している Device1 への参照をことができます。

-   IO を割り当てます\_削除\_Device1 に対応していますが、Device1 の拡張機能の外部で割り当てのロック構造体。
-   呼び出し[ **IoReleaseRemoveLockAndWait** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait) Device1 が削除されるときにします。
-   呼び出し[ **IoInitializeRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeremovelock) Device2 の削除ロックとして再利用する同じロックします。

後に手順 2. アプリケーションがいる可能性があります。 またはドライバーが引き続き Device1 への参照を保持します。 アプリケーションまたはドライバーが要求を送信できます Device1、場合でも、このデバイスが削除されました。 そのため、I/O マネージャー Device1 の削除されるまで、新しい削除ロックと同じメモリを再利用する安全ではありません。 別のスレッドがそれを取得しようとしたときに、同じロックを再初期化すると、ドライバーとシステム全体の予期しない結果に、ロックの破損可能性があります。

Windows 7、Windows オペレーティング システムの以降のバージョンで[I/O の検証の強化された](enhanced-i-o-verification.md)I/O の検証を選択すると、自動的にアクティブ化します。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバの I/O の検証機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドライン。**

    、コマンドラインでは、I/O の検証オプションで表される**ビット 4 (0x10)** します。 I/O の検証を有効にするには、0x10 のフラグの値を使用して、または 0x10 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x10 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows 2000 で使用することができます、 **/iolevel**のみレベル 1 (既定値) または両方のレベル 1 および Level 2 をアクティブ化のパラメーター。 以降のバージョンの Windows では、レベル 1 および Level 2 の両方が常にアクティブ化される I/O の検証を有効にするとします。

    たとえば、次のコマンドでは、Windows 2000 を実行するコンピューター上のレベル 1 およびレベル 2 の I/O の検証がアクティブにします。

    ```
    verifier /flags 0x10 /iolevel 2 /driver MyDriver.sys
    ```

    Windows Vista と Windows の以降のバージョンもアクティブ化し、I/O の検証を追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x10 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    I/O の検証機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    2.  選択**完全な一覧から個々 の設定を選択します。** します。
    3.  選択 (チェック) **I/O の検証**です。

    I/O の検証機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





