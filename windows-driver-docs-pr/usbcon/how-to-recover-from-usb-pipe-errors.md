---
Description: このトピックでは、USB パイプへのデータ転送が失敗した場合に試すことができる手順について説明します。 このトピックで説明するメカニズムでは、一括、割り込み、およびアイソクロナスパイプでのポート操作の中止、リセット、およびサイクルについて説明します。
title: USB パイプ エラーからの回復方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecafc26935b8bc71ffd8d068491febc1590a9b61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844370"
---
# <a name="how-to-recover-from-usb-pipe-errors"></a>USB パイプ エラーからの回復方法


このトピックでは、USB パイプへのデータ転送が失敗した場合に試すことができる手順について説明します。 このトピックで説明するメカニズムでは、一括、割り込み、およびアイソクロナスパイプでのポート操作の中止、リセット、およびサイクルについて説明します。

USB クライアントドライバーは、既定のエンドポイントに制御転送を送信することで、デバイスと通信します。デバイスの一括、割り込み、およびアイソクロナスエンドポイントへのデータ転送。 場合によっては、エンドポイントの失速条件など、さまざまな理由によって転送が失敗することがあります。 転送が失敗した場合、関連付けられているパイプは、エラー状態がクリアされるまで要求を処理できません。

制御転送の場合、USB ドライバースタックによってエラー状態が自動的にクリアされます。 データ転送の場合、クライアントはエラー状態から回復するための適切な手順を実行する必要があります。 データ転送が失敗すると、USB ドライバースタックは、失敗した USBD 状態コードを使用して、クライアントドライバーにエラーを報告します。 ドライバーは、状態コードに基づいてエラー回復メカニズムを提供できます。

このトピックでは、これらの操作によるエラー回復に関するガイドラインを示します。

-   USB パイプをリセットする
-   デバイスが接続されている USB ポートをリセットする
-   USB ポートを循環してクライアントドライバーのデバイススタックを再列挙する

エラー状態をクリアするには、パイプのリセット操作を開始し、必要な場合にのみ、リセットポートやサイクルポートなどのより複雑な操作を実行します。

<em>*さまざまな復旧メカニズムの調整について</em>*** : * *

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>クライアントドライバーは、回復のさまざまな操作を調整し、特定の時点で1つのメソッドのみが使用されるようにする必要があります。 たとえば、2つのエンドポイント (一括と割り込み) を持つデバイスを考えてみます。 デバイスにいくつかのデータ転送要求を送信した後、ドライバーは、一括パイプで要求が失敗したことを通知します。 これらのエラーから回復するために、ドライバーは一括パイプをリセットします。 ただし、この操作では転送エラーは解決されず、一括転送は失敗し続けます。 そのため、ドライバーは USB ポートをリセットする要求を発行します。 一方、割り込みパイプでの転送は失敗し、その後、デバイスのリセット要求が開始されます。 割り込み転送エラーから復旧するために、ドライバーは割り込みパイプでリセットパイプ要求を発行します。 これら2つの操作が調整されていない場合、ドライバーは両方のパイプの障害により、2つのリセットデバイス操作を同時に開始できます。 これらの同時操作は問題になる可能性があります。</p>
<p>クライアントドライバーは、一度に1つのリセットポートまたはサイクルポートの操作のみを実行するようにする必要があります。 これらの操作中、パイプではリセットパイプ操作が実行されていない必要があり、ドライバーは新しいリセットパイプ要求を発行できません。</p>
<p><em>Pankaj Gupta、Microsoft Windows USB コアチーム</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

-   クライアントドライバーによって、フレームワークの USB ターゲットデバイスオブジェクトが作成されている必要があります。

    Microsoft Visual Studio Professional 2012 で提供されている USB テンプレートを使用している場合は、テンプレートコードによってそれらのタスクが実行されます。 テンプレートコードは、ターゲットデバイスオブジェクトへのハンドルを取得し、デバイスコンテキストに格納します。

    KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「 [USB クライアントドライバーのコード構造 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)について」の「デバイスのソースコード」を参照してください。

-   クライアントドライバーは、フレームワークのターゲットパイプオブジェクトへのハンドルを持っている必要があります。 詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

<a name="instructions"></a>手順
------------

### <a href="" id="determine-the-cause-of-the-error-condition"></a>手順 1: エラー状態の原因を特定する

クライアントドライバーは、USB 要求ブロック (URB) を使用してデータ転送を開始します。 要求が完了すると、USB ドライバースタックから、転送が成功したか失敗したかを示す USBD ステータスコードが返されます。 エラーが発生した場合、USBD コードはエラーの原因を示します。

-   [**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッドを呼び出して urb を送信した場合は、メソッドが返された後に、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の**Hdr. Status**メンバーを確認します。
-   [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出して urb を非同期的に送信した場合は、 [*EVT_WDF_REQUEST_COMPLETION_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)で urb の状態を確認します。 *Params*パラメーターは、 [**WDF\_要求\_COMPLETION\_params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)構造体を指しています。 USBD の状態コードを確認するには、 **Usb&gt;UsbdStatus**メンバーを調べます。 コードの詳細については、「 [USBD\_STATUS](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539136(v=vs.85))」を参照してください。

転送エラーは、デバイスエラーが原因で発生する可能性があります。たとえば、USBD\_STATUS\_ストール\_PID や USBD\_STATUS\_バブル\_が検出されました。 また、ホストコントローラーによって報告されたエラー (USBD\_STATUS\_XACT\_ERROR など) が原因で発生することもあります。

### <a href="" id="determine-whether-the-device-is-connected-to-the-port"></a>手順 2: デバイスがポートに接続されているかどうかを確認する

パイプまたはデバイスをリセットする要求を発行する前に、デバイスが接続されていることを確認してください。 デバイスの接続状態を確認するには、 [**WdfUsbTargetDeviceIsConnectedSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous)メソッドを呼び出します。

### <a href="" id="cancel-all-pending-transfers-to-the-pipe"></a>手順 3: パイプへのすべての保留中の転送を取り消す

パイプまたはポートをリセットする要求を送信する前に、USB ドライバースタックがまだ完了していないパイプへのすべての保留中の転送要求を取り消します。 次のいずれかの方法で要求を取り消すことができます。

-   [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)メソッドを呼び出して、i/o ターゲットを停止します。

    I/o ターゲットを停止するには、まず、 [**WdfUsbTargetPipeGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget)メソッドを呼び出して、フレームワークパイプオブジェクトに関連付けられている WDFIOTARGET ハンドルを取得します。 ハンドルを使用して、 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出します。 この呼び出しで、アクションを**WdfIoTargetCancelSentIo**に設定します (「 [**WDF\_io\_TARGET\_SENT\_IO\_action**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action))」を参照して、USB ドライバースタックが完了していないすべての要求をキャンセルするようフレームワークに指示します。 完了した要求の場合、クライアントドライバーは、完了コールバックがフレームワークによって呼び出されるまで待機する必要があります。

-   中止パイプ要求を送信します。 次のいずれかのメソッドを呼び出すことによって、要求を送信できます。
    -   [**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)メソッドを呼び出します。

        この呼び出しは同期的であり、保留中のすべての要求が取り消された後にのみを返します。 [**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)は、省略可能な*要求*パラメーターを受け取ります。 WDFREQUEST ハンドルは、事前に割り当てられたフレームワークの要求オブジェクトに渡すことをお勧めします。 パラメーターを使用すると、ドライバーがアクセスできない内部要求オブジェクトではなく、指定された要求オブジェクトを使用できます。 このパラメーター値により、メモリ不足のために**WdfUsbTargetPipeAbortSynchronously**が失敗しないようにします。

    -   [**WdfUsbTargetPipeFormatRequestForAbort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)メソッドを呼び出して、abort パイプ要求の要求オブジェクトを書式設定し、 [**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出して要求を送信します。

        ドライバーが要求を非同期に送信する場合は、ドライバーが実装するドライバーの[*EVT_WDF_REQUEST_COMPLETION_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)へのポインターを指定する必要があります。 ポインターを指定するには、 [**Wdfrequestset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)メソッドを呼び出します。

        ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)で要求オプションの1つとして同期を\_\_オプションを送信\_\_を指定して、要求を同期的に送信できます。 要求を同期的に送信する場合は、代わりに[**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)を呼び出します。

### <a href="" id="reset-the-usb-pipe"></a>手順 4: USB パイプをリセットする

パイプをリセットして、エラー回復を開始します。 次のいずれかのメソッドを呼び出すことによって、リセットパイプ要求を送信できます。

-   [**WdfUsbTargetPipeResetSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)を呼び出して、リセットパイプ要求を同期的に送信します。
-   [**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)メソッドを呼び出して、リセットパイプ要求の要求オブジェクトを書式設定してから、 [**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出して要求を送信します。 これらの呼び出しは、手順 3. で説明されているように、abort パイプ要求のものに似ています。

**注**  は、パイプのリセット操作が完了するまで、新しい転送要求を送信しないようにしてください。

 

パイプのリセット要求によって、デバイスとホストコントローラーハードウェアのエラー状態がクリアされます。 デバイスエラーをクリアするために、USB ドライバースタックはエンドポイント\_HALT 機能セレクターを使用して、デバイスにクリア\_機能制御要求を送信します。 要求の受信者は、パイプに関連付けられているエンドポイントです。 アイソクロナスパイプでエラー状態が発生した場合、ドライバースタックはデバイスをクリアする操作を必要としません。これは、エラーが発生した場合に、アイソクロナスエンドポイントが自動的に消去されるためです。

ホストコントローラーエラーをクリアするには、ドライバースタックがパイプの停止状態をクリアし、パイプのデータ切り替えを0にリセットします。

### <a href="" id="reset-the-usb-port"></a>手順 5: USB ポートをリセットする

パイプのリセット操作でエラー状態が解決されず、データ転送が引き続き失敗する場合は、リセットポート要求を送信します。

1.  デバイスへのすべての転送を取り消します。 これを行うには、現在の構成のすべてのパイプを列挙し、各パイプに対してスケジュールされている保留中の要求を取り消します。
2.  デバイスの i/o ターゲットを停止します。

    [**WdfUsbTargetDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)メソッドを呼び出して、フレームワークターゲットデバイスオブジェクトに関連付けられている WDFIOTARGET ハンドルを取得します。 次に、 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出し、wdfiotarget ハンドルを指定します。 呼び出しで、アクションを**WdfIoTargetCancelSentIo** (WDF\_IO\_TARGET\_SENT\_IO\_action) に設定します。

3.  [**WdfUsbTargetDeviceResetPortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)メソッドを呼び出して、リセットポート要求を送信します。

リセットポート操作により、デバイスが USB バス上で再列挙されます。 USB ドライバースタックは、列挙後にデバイス構成を保持します。 ドライバースタックによって既存のパイプハンドルが有効なままであるため、クライアントドライバーは以前に取得したパイプハンドルを使用できます。

複合デバイスの個々の機能をリセットすることはできません。 複合デバイスの場合、特定の関数のクライアントドライバーがリセットポートの要求を送信すると、デバイス全体がリセットされます。 USB デバイスが状態を保持している場合、そのポートのリセット要求は、他の機能のクライアントドライバーに影響を与える可能性があります。 そのため、クライアントドライバーは、ポートをリセットする前にパイプのリセットを試行することが重要です。

### <a href="" id="cycle-the-usb-port"></a>手順 6: USB ポートを循環する

サイクルポートの操作は、デバイスが切断されていないことを除いて、取り外しられてポートに接続されているデバイスに似ています。 デバイスが切断され、ソフトウェアに再接続されます。 この操作は、デバイスのリセットと列挙につながります。 その結果、PnP マネージャーはデバイスノードを再構築します。

リセットポート操作でエラー状態が解決されず、データ転送が引き続き失敗する場合は、サイクルポート要求を送信します。

1.  デバイスへのすべての転送を取り消します。 現在の構成で、各パイプに対して保留中の要求がスケジュールされていることを確認してください (手順3を参照)。
2.  デバイスの i/o ターゲットを停止します。

    [**WdfUsbTargetDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)メソッドを呼び出して、フレームワークターゲットデバイスオブジェクトに関連付けられている WDFIOTARGET ハンドルを取得します。 次に、 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出し、wdfiotarget ハンドルを指定します。 呼び出しで、アクションを**WdfIoTargetCancelSentIo** (WDF\_IO\_TARGET\_SENT\_IO\_action) に設定します。

3.  次のいずれかの方法を呼び出して、サイクルポートの要求を送信します。
    -   [**WdfUsbTargetDeviceCyclePortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously)を呼び出して、循環ポート要求を同期的に送信します。
    -   [**WdfUsbTargetDeviceFormatRequestForCyclePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport)メソッドを呼び出して、循環ポート要求の要求オブジェクトを書式設定し、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出して要求を送信します。 これらの呼び出しは、手順 3. で説明されているように、abort パイプ要求のものに似ています。

クライアントドライバーは、サイクルポートの要求が完了した後にのみ、デバイスに転送要求を送信できます。 これは、USB ドライバースタックが循環ポート要求を処理している間に、デバイスノードが削除されるためです。

サイクルポートの要求により、デバイスが再列挙されます。 USB ドライバースタックは、デバイスが切断されたことを PnP マネージャーに通知します。 PnP マネージャーは、クライアントドライバーに関連付けられているデバイススタックを破棄します。 ドライバースタックは、デバイスをリセットし、USB バス上で再列挙し、デバイスが接続されたことを PnP マネージャーに通知します。 PnP マネージャーは、USB デバイスのデバイススタックを再構築します。

サイクルポート操作の結果として、デバイスに対してハンドルが開かれているアプリケーションは、デバイス削除通知を取得します (このような通知にアプリケーションが登録されている場合)。 応答として、アプリケーションは、デバイスが接続されていないメッセージをユーザーに報告する場合があります。 クライアントドライバーは、ユーザーエクスペリエンスに影響を与えるため、他の復旧メカニズムによってエラー状態が解決されない場合にのみ、サイクルポートの要求を選択する必要があります。

(手順6で説明されている) ポートのリセット操作と同様に、複合デバイスの場合は、デバイスの個々の機能ではなく、デバイス全体に影響します。

## <a name="related-topics"></a>関連トピック
[USB i/o 転送](usb-device-i-o.md)  



