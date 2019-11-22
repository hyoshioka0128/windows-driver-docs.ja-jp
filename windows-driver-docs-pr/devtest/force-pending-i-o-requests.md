---
title: 保留中の I/O 要求を強制する
description: 保留中の I/O 要求を強制する
ms.assetid: 0255fc5c-0e75-4108-ba29-f1a61ce9b0dd
keywords:
- 強制的に保留中の i/o 要求オプション WDK ドライバー検証ツール
- WDK Driver Verifier の STATUS_PENDING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2fee6906e7c8863ea91767ea19b43834e7760b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840270"
---
# <a name="force-pending-io-requests"></a>保留中の I/O 要求を強制する


Force Pending i/o Requests オプションは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)へのドライバーの呼び出しに応答して、\_状態をランダムに返します。 このオプションは、 **IoCallDriver**からの保留中の戻り値\_状態に応答するドライバーのロジックをテストします。

このオプションは、windows Vista 以降のバージョンの Windows オペレーティングシステムでのみサポートされています。

**注意**   ドライバーの操作に関する詳細な知識があり、 **IoCallDriver**のすべての呼び出しから保留中の戻り値\_状態を処理するようにドライバーが設計されていることを確認している場合を除き、このオプションをドライバーで使用しないでください。 このオプションをすべての呼び出しから保留中の状態\_処理するように設計されていないドライバーで実行すると、クラッシュ、メモリの破損、異常なシステムの動作が発生し、デバッグや修正が困難になる可能性があります。

 

### <a name="span-idwhy_use_force_pending_i_o_requests_spanspan-idwhy_use_force_pending_i_o_requests_spanwhy-use-force-pending-io-requests"></a><span id="why_use_force_pending_i_o_requests_"></span><span id="WHY_USE_FORCE_PENDING_I_O_REQUESTS_"></span>強制的に保留中の i/o 要求を使用するのはなぜですか。

ドライバースタック内の上位レベルのドライバーは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)をドライバースタック内の下位レベルのドライバーに渡すために、を呼び出します。 IRP を受信する下位レベルのドライバーのドライバーディスパッチルーチンは、IRP を直ちに完了するか、または状態\_PENDING を返して後で IRP を完了することができます。

通常、呼び出し元は、いずれかの結果を処理できるように準備する必要があります。 ただし、ほとんどのディスパッチルーチンは IRP をすぐに処理するので、呼び出し元の状態\_保留中のロジックは実行されず、重大な論理エラーが検出されない可能性があります。 Force Pending i/o Requests オプションは、 **IoCallDriver**への呼び出しをインターセプトし、STATUS\_Pending を返して、呼び出し元ドライバーの使用頻度が低いロジックをテストします。

### <a name="span-idwhen_do_you_use_force_pending_i_o_requests_spanspan-idwhen_do_you_use_force_pending_i_o_requests_spanwhen-do-you-use-force-pending-io-requests"></a><span id="when_do_you_use_force_pending_i_o_requests_"></span><span id="WHEN_DO_YOU_USE_FORCE_PENDING_I_O_REQUESTS_"></span>強制的に保留中の i/o 要求を使用するのはどのような場合ですか。

このテストを実行する前に、ドライバーの設計とソースコードを確認し、すべての[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)呼び出しから保留中の状態\_処理するようにドライバーが想定されていることを確認します。

多くのドライバーは、 **IoCallDriver**のすべての呼び出しで状態\_保留中に処理されるように設計されていません。 Irp をすぐに完了することが保証されている特定の既知のドライバーに IRP を送信する場合があります。 状態\_保留中のドライバーに送信すると、ドライバーとシステムのクラッシュやメモリの破損が発生する可能性があります。

### <a name="span-idhow_should_drivers_handle_status_pending_spanspan-idhow_should_drivers_handle_status_pending_spanhow-should-drivers-handle-status_pending"></a><span id="how_should_drivers_handle_status_pending_"></span><span id="HOW_SHOULD_DRIVERS_HANDLE_STATUS_PENDING_"></span>ドライバーがステータス\_保留中に処理する方法

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す上位レベルのドライバーは、次のように状態\_保留中の戻り値を処理する必要があります。

-   **IoCallDriver**を呼び出す前に、ドライバーは[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)を呼び出して、IRP の同期処理を調整する必要があります。

-   **IoCallDriver**が PENDING\_を返した場合、ドライバーは、指定されたイベントに対して[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出すことによって、IRP の完了を待機する必要があります。

-   ドライバーは、i/o マネージャーがイベントを通知する前に、IRP が解放される可能性があることを予測する必要があります。

-   **IoCallDriver**を呼び出した後、呼び出し元は IRP を参照できません。

### <a name="span-idwhich_errors_does_force_pending_i_o_request_detect_spanspan-idwhich_errors_does_force_pending_i_o_request_detect_spanwhich-errors-does-force-pending-io-request-detect"></a><span id="which_errors_does_force_pending_i_o_request_detect_"></span><span id="WHICH_ERRORS_DOES_FORCE_PENDING_I_O_REQUEST_DETECT_"></span>保留中の i/o 要求を強制的に検出するエラーは何ですか。

Force Pending i/o Request オプションは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出し、保留状態の戻り値\_状態を受け取る、ドライバー内の次のエラーを検出します。

-   ドライバーは、同期処理のために**IoBuildSynchronousFsdRequest**を呼び出しません。

-   ドライバーは**KeWaitForSingleObject**を呼び出しません。

-   ドライバーは、 **IoCallDriver**を呼び出した後に、IRP 構造体の値を参照します。 **IoCallDriver**を呼び出した後、より高いレベルのドライバーは、完了ルーチンを設定した場合を除き、irp にアクセスすることはできません。その後、すべての下位レベルのドライバーが irp を完了したときのみです。 IRP が解放されると、ドライバーがクラッシュします。

-   ドライバーが関連する関数を正しく呼び出しません。 たとえば、ドライバーは**KeWaitForSingleObject**を呼び出し、イベントオブジェクトへのポインターを渡すのではなく、(*オブジェクト*パラメーターとして) イベントにハンドルを渡します。

-   ドライバーは、間違ったイベントを待機します。 たとえば、ドライバーは**Iosetcompletion ルーチン**を呼び出しますが、irp の完了時に i/o マネージャーによって通知される irp イベントを待機するのではなく、独自の完了ルーチンによって通知される内部イベントを待機します。

### <a name="span-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanspan-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanspan-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanforce-pending-io-requests-changes-introduced-in-windows-7"></a><span id="Force_Pending_I_O_Requests_Changes_Introduced_in_Windows_7"></span><span id="force_pending_i_o_requests_changes_introduced_in_windows_7"></span><span id="FORCE_PENDING_I_O_REQUESTS_CHANGES_INTRODUCED_IN_WINDOWS_7"></span>Windows 7 で導入された保留中の i/o 要求の変更を強制する

Windows 7 以降では、[保留中の i/o 要求を強制する] オプションの方が、検証されたドライバーで保留中のコードパス\_状態を強制する場合により効果的です。 以前のバージョンの Windows では、ドライバーの検証ツールは、その IRP の最初の[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)が実行されるときにのみ、irp の完了を強制的に遅延させていました。 これは、同じデバイススタックからの Driver2 の動作によって、Driver1 を検証する効果を減らすことができることを意味します。 Driver2 は、ディスパッチルーチンから Driver1 に戻る前に、同期的に完了するまで待機することがあります。 IRP 完了の強制遅延は、i/o 要求が完了パスで検証されたドライバーに戻される前に正確に発生します。 これは、検証されたドライバーの状態\_保留中のコードパスを実際に実行し、検証されたドライバーが完了までの遅延を認識することを意味します。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

強制保留中の i/o 要求をアクティブ化するには、 [I/o 検証](i-o-verification.md)もアクティブ化する必要があります。 1つまたは複数のドライバーに対して、Driver Verifier マネージャーまたは Verifier コマンドラインを使用して、[強制的に保留中の i/o 要求] オプションをアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

強制的に保留中の i/o 要求オプションは、Windows Vista 以降のバージョンの Windows でのみサポートされています。

-   **コマンドラインで**

    強制保留中の i/o 要求をアクティブにするには、フラグ値0x210 を使用するか、または0x210 をフラグ値に追加します。 この値は、i/o 検証 (0x10) をアクティブにし、強制的に保留中の i/o 要求 (0x200) を実行します。

    次に、例を示します。

    ```
    verifier /flags 0x210 /driver MyDriver.sys
    ```

    オプションは、次回の起動時にアクティブになります。

    強制保留中の i/o 要求 (verifier/flags 0x200) のみをアクティブ化しようとすると、ドライバー検証ツールは強制的に保留中の i/o 要求 (0x200) と[I/o 検証](i-o-verification.md)の両方を自動的に有効にします。

    コマンドに/volatile パラメーターを追加することで、コンピューターを再起動せずに、強制的に保留中の i/o 要求をアクティブ化および非アクティブ化することもできます。 次に、例を示します。

    ```
    verifier /volatile /flags 0x210 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  [ [I/o 検証](i-o-verification.md)] を選択し、保留中の i/o 要求を強制的に実行します。

    **強制的に保留中の I/o 要求**のみを選択した場合は、ドライバー検証マネージャーによって、I/o の[確認](i-o-verification.md)が必要であることが通知され、それを有効にするためのが提供されます。

### <a name="span-idviewing_the_resultsspanspan-idviewing_the_resultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果の表示

Force Pending i/o Requests テストの結果を表示するには、 **! verifier**デバッガー拡張機能とフラグ値0x40 を使用します。

**! Verifier**の詳細については、 *Windows 用デバッグツール*のドキュメントの **! verifier**に関するトピックを参照してください。

Force Pending i/o Requests テストの結果としてテストコンピューターがクラッシュした場合は、 **! verifier 40**コマンドを使用して原因を見つけることができます。 現在のスタックトレースで、ドライバーによって最近使用された IRP のアドレスを検索します。 たとえば、スレッドのスタックフレームを表示する**kP**コマンドを使用すると、現在のスタックトレースの関数パラメーターの中で IRP アドレスを見つけることができます。 次に、 **! verifier 40**を実行し、IRP のアドレスを探します。 最新の保留中のスタックトレースは、画面の上部に表示されます。

たとえば、Pci の次のスタックトレースは、保留中の i/o 要求を強制的に実行する応答を示しています。 テストでは、Pci のロジックでエラーが発生することはありません。

```
kd> !verifier 40
# Size of the log is 0x40
========================================================
IRP: 8f84ef00 - forced pending from stack trace:

     817b21e4 nt!IovpLocalCompletionRoutine+0xb2
     81422478 nt!IopfCompleteRequest+0x15c
     817b2838 nt!IovCompleteRequest+0x9c
     84d747df acpi!ACPIBusIrpDeviceUsageNotification+0xf5
     84d2d36c acpi!ACPIDispatchIrp+0xe8
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     817c6a9d nt!ViFilterDispatchPnp+0xe9
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84fed489 pci!PciCallDownIrpStack+0xbf
     84fde1cb pci!PciDispatchPnpPower+0xdf
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     817c6a9d nt!ViFilterDispatchPnp+0xe9
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84ff2ff5 pci!PciSendPnpIrp+0xbd
 84fec820 pci!PciDevice_DeviceUsageNotification+0x6e
     84fde1f8 pci!PciDispatchPnpPower+0x10c
 817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84d76ce2 acpi!ACPIFilterIrpDeviceUsageNotification+0x96
     84d2d36c acpi!ACPIDispatchIrp+0xe8
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84f7f16c PCIIDEX!PortWdmForwardIrpSynchronous+0x8e
     84f7b2b3 PCIIDEX!GenPnpFdoUsageNotification+0xcb
     84f7d301 PCIIDEX!PciIdeDispatchPnp+0x45
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
```

スタックトレースは、 *Acpi*が IRP 8f84 ef00 を完了しようとしていることを示しています。 ドライバーの検証ツールによって遅延完了が強制されたため、 *Acpi*によってステータス\_が保留中に pci に戻されました。 **PciCallDownIrpStack**。 この呼び出しでクラッシュが発生した場合、ドライバーの所有者は pci のソースコードを確認する必要があります **。PciCallDownIrpStack**を変更し、正常に保留中のステータス\_を処理します。

 

 





