---
title: 保留中の I/O 要求を強制する
description: 保留中の I/O 要求を強制する
ms.assetid: 0255fc5c-0e75-4108-ba29-f1a61ce9b0dd
keywords:
- 保留中の I/O 要求を強制 WDK Driver Verifier をオプションします。
- STATUS_PENDING WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 980c325c5f1627c2fd18404f34e55b59c433a57c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577859"
---
# <a name="force-pending-io-requests"></a>保留中の I/O 要求を強制する


保留中の I/O 要求を Force オプションがランダムにステータスを返します\_にドライバーの呼び出しに応答 PENDING [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 このオプションの状態に対応するため、ドライバーのロジックをテストする\_PENDING から値を返す**保留**します。

このオプションは、Windows Vista および Windows オペレーティング システムの以降のバージョンでのみサポートされます。

**注意**  ドライバーの動作のサポート技術情報の詳細なし、ドライバーが状態を処理するために設計されていることを確認する場合は、ドライバーでこのオプションを使用しない\_への呼び出しのすべてからの戻り値をPENDING**保留**します。 ドライバーでこのオプションを実行しているは、状態を処理するものはありません\_のすべての呼び出しからの保留により、クラッシュ、メモリの破損、およびシステムの異常な動作をデバッグまたは修正で難しい場合があります。

 

### <a name="span-idwhyuseforcependingiorequestsspanspan-idwhyuseforcependingiorequestsspanwhy-use-force-pending-io-requests"></a><span id="why_use_force_pending_i_o_requests_"></span><span id="WHY_USE_FORCE_PENDING_I_O_REQUESTS_"></span>保留中の I/O 要求の強制を使用する理由

ドライバーより高度なドライバー スタック呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)ドライバー スタック内に下位レベルのドライバーは IRP を渡す。 IRP を受信する下位レベルのドライバーのドライバーのディスパッチ ルーチンは IRP を直ちに完了または状態を返す\_PENDING IRP を後で完了するとします。

通常、呼び出し元は、いずれかの結果を処理する準備である必要があります。 ただし、ほとんどをディスパッチするために、ルーチン処理 IRP をすぐに、状態\_保留中の呼び出し側のロジックは多くの場合、実行されると、重大なロジックがエラーを検出しない可能性があります。 保留中の I/O 要求を Force オプションへの呼び出しをインターセプト**保留**ステータスを返す\_保留中の呼び出しをテストするドライバー使用頻度の低いロジック。

### <a name="span-idwhendoyouuseforcependingiorequestsspanspan-idwhendoyouuseforcependingiorequestsspanwhen-do-you-use-force-pending-io-requests"></a><span id="when_do_you_use_force_pending_i_o_requests_"></span><span id="WHEN_DO_YOU_USE_FORCE_PENDING_I_O_REQUESTS_"></span>Force 保留中の I/O 要求を使用する場合

このテストを実行する前に、ドライバーのデザインとソース コードを確認し、ドライバーが状態を処理するものであることを確認します。\_からすべての保留、 [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)呼び出し。

ドライバーの数が状態を処理するために設計されていません\_に対するすべての呼び出しで保留**保留**します。 IRP これら IRP を直ちに完了する保証は特定のよく知られているドライバーに送信される可能性があります。 送信ステータス\_PENDING 処理をしないドライバーをドライバーとシステムのクラッシュとメモリの破損が発生することができます。

### <a name="span-idhowshoulddrivershandlestatuspendingspanspan-idhowshoulddrivershandlestatuspendingspanhow-should-drivers-handle-statuspending"></a><span id="how_should_drivers_handle_status_pending_"></span><span id="HOW_SHOULD_DRIVERS_HANDLE_STATUS_PENDING_"></span>ドライバーを処理する方法の状態\_PENDING でしょうか。

呼び出すより高度なドライバー [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) 、状態を処理する必要があります\_PENDING 戻り値が次のようにします。

-   呼び出しの前に**保留**、ドライバーを呼び出す必要があります[ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)に IRP の同期処理を調整します。

-   場合**保留**ステータスを返します\_保留中のドライバーは呼び出すことによって待機 IRP が完了する必要があります[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)指定しました。イベントです。

-   ドライバーは、I/O マネージャーは、イベントを通知する前に、IRP を解放する場合がありますを予測する必要があります。

-   呼び出した後**保留**、呼び出し元は IRP を参照できません。

### <a name="span-idwhicherrorsdoesforcependingiorequestdetectspanspan-idwhicherrorsdoesforcependingiorequestdetectspanwhich-errors-does-force-pending-io-request-detect"></a><span id="which_errors_does_force_pending_i_o_request_detect_"></span><span id="WHICH_ERRORS_DOES_FORCE_PENDING_I_O_REQUEST_DETECT_"></span>保留中の I/O 要求の強制はエラーを検出しますか。

保留中の I/O 要求を Force オプションを呼び出すドライバーで、次のエラーを検出した[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)ステータスを受信および\_PENDING 戻り値。

-   ドライバーは呼び出しません**IoBuildSynchronousFsdRequest**に同期処理を調整します。

-   ドライバーは呼び出しません**kewaitforsingleobject の 1**します。

-   呼び出した後、IRP 構造内の値を参照してドライバー**保留**します。 呼び出した後**保留**、完了ルーチンを設定していない限りより高度なドライバーは IRP をアクセスことはできませんし、のみ完了すると低レベルのすべてのドライバーが IRP します。 IRP が解放されると、ドライバーがクラッシュします。

-   ドライバーに呼び出す related 関数正しくします。 たとえば、ドライバーが呼び出す**kewaitforsingleobject の 1**イベントを識別するハンドルを渡します (として、*オブジェクト*パラメーター)、イベント オブジェクトへのポインターを渡す代わりにします。

-   ドライバーは、正しくないイベントを待機します。 たとえば、ドライバーが呼び出す**IoSetCompletionRoutine**が IRP イベント IRP の完了時に I/O マネージャーによってがシグナルを待機してではなく、独自の完了ルーチンによって通知される内部イベントを待ちます。

### <a name="span-idforcependingiorequestschangesintroducedinwindows7spanspan-idforcependingiorequestschangesintroducedinwindows7spanspan-idforcependingiorequestschangesintroducedinwindows7spanforce-pending-io-requests-changes-introduced-in-windows-7"></a><span id="Force_Pending_I_O_Requests_Changes_Introduced_in_Windows_7"></span><span id="force_pending_i_o_requests_changes_introduced_in_windows_7"></span><span id="FORCE_PENDING_I_O_REQUESTS_CHANGES_INTRODUCED_IN_WINDOWS_7"></span>導入された Windows 7 を強制的に保留中の I/O 要求の変更

Windows 7 以降、Force 保留中の I/O 要求オプションを効率的に強制的に状態のテストを実行する\_保留中の検証済みのドライバーのコード パス。 以前の Windows バージョンでは、Driver Verifier 強制、IRP の完了が遅延する場合にのみ、最初[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)の IRP を実行します。 つまり、同じデバイス スタックから Driver1 の検証の有効性が Driver2 の動作によって削減できます。 Driver1 のディスパッチ、ルーチンに返す前に同期的に Driver2 を待機し、完了する可能性があります。 I/O 要求が入力候補のパスの検証済みのドライバーにアンワインドする前に正確に IRP の完了の強制の遅延が発生します。 つまり、ステータス\_検証済みのドライバーのパスが実際に実行された保留中のコードと検証済みのドライバーが完了するまでの遅延を認識します。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

Force 保留中の I/O 要求をアクティブ化する必要がありますもアクティブ化する[I/O の検証](i-o-verification.md)です。 ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーの保留中の I/O 要求を Force オプションをアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

保留中の I/O 要求を Force オプションは、Windows Vista および Windows の以降のバージョンでのみサポートされます。

-   **コマンドラインで**

    Force 保留中の I/O 要求をアクティブ化するには、0x210 のフラグの値を使用するか、フラグの値に 0x210 を追加します。 この値には、I/O の検証 (0x10) および Force 保留中の I/O 要求 (0x200) がアクティブにします。

    例:

    ```
    verifier /flags 0x210 /driver MyDriver.sys
    ```

    オプションは、[次へ] の起動後にアクティブになります。

    アクティブのみ強制保留中の I/O 要求 (verifier/flags 0x200) ドライバーの検証ツールが自動的に両方 Force 保留中の I/O 要求 (0x200) を有効にしようとすると、 [I/O の検証](i-o-verification.md)です。

    また、アクティブ化し、/volatile を追加することで、コンピューターを再起動しなくても強制保留中の I/O 要求を非アクティブ化パラメーターをコマンド。 以下に例を示します。

    ```
    verifier /volatile /flags 0x210 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**、順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択[I/O の検証](i-o-verification.md)と保留中の I/O 要求を強制します。

    のみを選択した場合**Force 保留中の I/O 要求**、ドライバー検証マネージャー通知を[I/O の検証](i-o-verification.md)を有効にされておりが必要です。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果を表示します。

Force 保留中の I/O 要求のテストの結果を表示する、 **! verifier**デバッガー拡張機能で、フラグ値 0x40 です。

について **! verifier**を参照してください、 **! verifier**でトピック、*ツールを Windows のデバッグ*ドキュメント。

Force 保留中の I/O 要求のテストの結果として、テスト マシンがクラッシュした場合は使用できます、 **! verifier 40**原因を特定するコマンド。 現在のスタック トレースで、ドライバーによって最近使用された IRP のアドレスを見つけます。 使用する場合など、 **kP**コマンドで、スレッドのスタック フレームを表示する現在のスタック トレースの関数パラメーターの間で IRP アドレスを見つけることができます。 実行し **! verifier 40** IRP のアドレスを検索するとします。 ディスプレイ画面の上部にある保留中のスタック トレース、最新の強制が表示されます。

たとえば、Pci.sys の次のスタック トレースは、Force 保留中の I/O 要求の応答を示します。 テストでは、Pci.sys ロジックのエラーは表示されません。

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

スタック トレースを表示する*Acpi.sys* IRP 8f84ef00 を完了しようとします。 Driver Verifier は、遅延の入力候補のため強制*Acpi.sys*状態が返されました\_を PENDING **pci!PciCallDownIrpStack**します。 ソース コードを確認するドライバーの所有者になる場合、この呼び出しには、クラッシュが原因となったが、 **pci!PciCallDownIrpStack**状態を処理するために改訂および\_PENDING 適切です。

 

 





