---
Description: このトピックでは、ときに、USB パイプへのデータ転送を試みることができますの手順については失敗します。 このトピックでカバーで説明されているメカニズムは、中止、リセットして、一括、割り込み、アイソクロナス パイプでポート operations のサイクルします。
title: USB パイプ エラーからの回復方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df58d4e869dd4f86ecc8f411dd80ba4fbb880712
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363917"
---
# <a name="how-to-recover-from-usb-pipe-errors"></a>USB パイプ エラーからの回復方法


このトピックでは、ときに、USB パイプへのデータ転送を試みることができますの手順については失敗します。 このトピックでカバーで説明されているメカニズムは、中止、リセットして、一括、割り込み、アイソクロナス パイプでポート operations のサイクルします。

USB クライアント ドライバーは、コントロールの転送を既定のエンドポイントに送信することによって、そのデバイスと通信します。データは、一括、割り込み、およびデバイスのアイソクロナス エンドポイントに転送します。 エンドポイントの停止条件などのさまざまな理由により、その転送は失敗します。 転送が失敗すると、関連するパイプは、エラー状態がクリアされるまでに要求を処理できません。

コントロール転送の場合は、USB ドライバー スタックは、エラー条件を自動的にクリアします。 データ転送の場合、クライアントは、エラー条件から回復する適切な手順を実行する必要があります。 データ転送が失敗した場合、USB ドライバー スタックは、失敗した USBD 状態コードを使ってクライアント ドライバーにエラーを報告します。 状態コードに基づいて、ドライバーはできるエラー回復メカニズムを提供し。

このトピックでは、これらの操作により、エラーの回復に関するガイドラインを提供します。

-   USB パイプをリセットします。
-   デバイスが接続されている USB ポートをリセットします。
-   クライアント ドライバーのデバイス スタックを再列挙するために USB ポートをサイクルします。

エラー状態をクリアするにリセット パイプ操作を開始し、必要がある場合にのみ、リセット ポート サイクル-ポートなどのより複雑な操作を実行します。

<em>***さまざまな復旧のメカニズムを調整</em>* : * *

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>クライアント ドライバーは、復旧のさまざまな操作を調整して、特定の時点で 1 つのメソッドが使用されるようにする必要があります。 たとえば、2 つのエンドポイントを使用したデバイス: 一括と割り込みです。 いくつかのデータ転送の要求を送信すると、デバイスに、ドライバーの通知を要求するは、一括パイプで失敗します。 これらのエラーから回復するには、ドライバーは、一括パイプをリセットします。 ただし、その操作が引き続き失敗すると、転送エラーと一括転送を解決できません。 そのため、ドライバーは、USB ポートにリセットする要求を発行します。 一方、割り込みのパイプ、および、その後デバイスのリセット要求に失敗する、転送が開始します。 割り込みの転送エラーから回復するには、ドライバーは、割り込みパイプでリセット パイプ要求を発行します。 これら 2 つの操作が調整された場合は、ドライバーを開始できます 2 つのデバイスのリセット操作に同時に、両方のパイプに失敗したため。 これらの同時操作は、問題が発生することができます。</p>
<p>クライアント ドライバーは、特定の時点で、ドライバー操作が実行される 1 つだけリセット ポートまたはサイクル ポートのことを確認してください。 これらの操作中にリセット パイプ操作は、任意のパイプで進行状況ですることはできませんし、ドライバーでは、新しいパイプ リセット要求は発行する必要があります。</p>
<p><em>Pankaj Gupta、Microsoft Windows USB コア チーム</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

-   クライアント ドライバー フレームワーク USB ターゲット デバイス オブジェクトを作成する必要があります。

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。

    KMDF クライアント ドライバーは、呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッド。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。

-   クライアント ドライバーでは、フレームワーク ターゲットのパイプ オブジェクトを識別するハンドルが必要です。 詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

<a name="instructions"></a>手順
------------

### <a href="" id="determine-the-cause-of-the-error-condition"></a>手順 1:エラー状態の原因を判断します。

クライアント ドライバーでは、USB 要求ブロック (URB) を使用して、データ転送を開始します。 要求が完了すると、USB ドライバー スタックは、転送が成功したか、失敗したかどうかを示す USBD ステータス コードを返します。 発生するでは、USBD コードは、失敗の理由を示します。

-   呼び出して URB を送信した場合、 [ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッド、チェック、 **Hdr.Status**のメンバー、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)メソッドが返された後構造体します。
-   呼び出すことによって、URB を非同期的に送信した場合、 [ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド、URB 状態を確認、 [ *EVT_WDF_REQUEST_COMPLETION_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine). *Params*パラメーターが指す、 [ **WDF\_要求\_完了\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)構造体。 USBD ステータス コードを確認するには、検査、 **Usb -&gt;UsbdStatus**メンバー。 コードについては、次を参照してください。 [USBD\_状態](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539136(v=vs.85))します。

USBD など、デバイスのエラーからの転送エラーが発生\_状態\_失速\_PID または USBD\_状態\_BABBLE\_が検出されました。 ホスト コント ローラーの USBD などによって報告されたエラーのため発生する可能性も\_状態\_XACT\_エラー。

### <a href="" id="determine-whether-the-device-is-connected-to-the-port"></a>手順 2:デバイスがポートに接続されているかどうかを判断します。

パイプ デバイスをリセットするすべての要求を発行する前に、デバイスが接続されていることを確認します。 呼び出すことによって、デバイスの接続状態を調べる、 [ **WdfUsbTargetDeviceIsConnectedSynchronous** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous)メソッド。

### <a href="" id="cancel-all-pending-transfers-to-the-pipe"></a>手順 3:パイプへのすべての保留中の転送をキャンセルします。

ポートまたはパイプをリセットするすべての要求を送信する前に、パイプでは、USB ドライバー スタックがまだ完了していないすべての保留中の転送要求をキャンセルします。 次の方法のいずれかで要求をキャンセルできます。

-   I/O ターゲットを呼び出すことによって停止、 [ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)メソッド。

    I/O ターゲットを停止するには、最初に、呼び出して framework パイプ オブジェクトに関連付けられている WDFIOTARGET ハンドルを取得、 [ **WdfUsbTargetPipeGetIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget)メソッド。 ハンドルを使用すると、呼び出す[ **WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)します。 呼び出しでアクションを設定**WdfIoTargetCancelSentIo** (を参照してください[ **WDF\_IO\_ターゲット\_SENT\_IO\_アクション** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action)) USB ドライバー スタックが完了していないすべての要求を取り消すために、フレームワークに指示します。 完了した要求の場合、クライアント ドライバーにフレームワークによって呼び出される場合は、その完了コールバックを待つ必要があります。

-   中止パイプ要求を送信します。 これらのメソッドのいずれかを呼び出すことによって、要求を送信できます。
    -   呼び出す、 [ **WdfUsbTargetPipeAbortSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)メソッド。

        呼び出しが同期され返しますのみすべて保留中の要求は取り消されます。 [**WdfUsbTargetPipeAbortSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)は省略可能な*要求*パラメーター。 事前に割り当てられる framework 要求オブジェクトに WDFREQUEST ハンドルを渡すことをお勧めします。 パラメーターは、使用のフレームワークは、ドライバーがアクセスできない内部要求オブジェクトではなく、指定された要求オブジェクトを使用します。 このパラメーターの値により**WdfUsbTargetPipeAbortSynchronously**メモリ不足が原因で失敗しません。

    -   呼び出す、 [ **WdfUsbTargetPipeFormatRequestForAbort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)メソッドは、パイプの中止の要求の要求オブジェクトを書式設定を呼び出すことによって、要求を送信[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。

        ドライバーは、非同期的に要求を送信する場合、ドライバーへのポインターを指定する必要があります[ *EVT_WDF_REQUEST_COMPLETION_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)ドライバーを実装します。 ポインターを指定するには、呼び出し、 [ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)メソッド。

        ドライバーは WDF を指定することで、要求を同期的に送信できます\_要求\_送信\_オプション\_同期で、要求オプションの 1 つとして[ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend). 同期的に、要求を送信する場合、呼び出す[ **WdfUsbTargetPipeAbortSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)代わりにします。

### <a href="" id="reset-the-usb-pipe"></a>手順 4:USB パイプをリセットします。

パイプをリセットすることで、エラーからの回復を開始します。 これらのメソッドのいずれかを呼び出すことによってリセット パイプ要求を送信することができます。

-   呼び出す、 [ **WdfUsbTargetPipeResetSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)パイプのリセット要求を同期的に送信します。
-   呼び出す、 [ **WdfUsbTargetPipeFormatRequestForReset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)メソッドは、リセット パイプ要求の要求オブジェクトを書式設定を呼び出すことによって、要求を送信[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。 これらの呼び出しは、手順 3. で説明したように、中止パイプ要求に似ています。

**注**  リセット パイプ操作が完了するまで新しい要求を転送いずれかを送信しません。

 

リセット パイプ要求は、デバイスとホスト コント ローラーのハードウェアのエラー条件をクリアします。 USB ドライバー スタックが、明確なを送信するデバイスのエラーをクリアする\_機能コントロール要求をエンドポイントを使用してデバイス\_停止機能セレクター。 要求の受信者は、パイプに関連付けられているエンドポイントです。 アイソクロナス パイプでエラーが発生した場合、ドライバー スタックを行わず、エラーが発生アイソクロナス エンドポイントが自動的に消去するために、デバイスをオフにします。

ホスト コント ローラーのエラーをクリアするには、ドライバー スタックは、パイプの停止の状態をクリアし、パイプのデータの切り替えを 0 にリセットします。

### <a href="" id="reset-the-usb-port"></a>手順 5:USB ポートをリセットします。

リセット パイプ操作がエラー状態をクリアしないデータ転送は引き続き失敗する場合は、ポートをリセット要求を送信します。

1.  デバイスへのすべての転送をキャンセルします。 これを行うには、現在の構成内のすべてのパイプを列挙し、保留中の各パイプのスケジュール要求をキャンセルします。
2.  デバイスの I/O ターゲットを停止します。

    呼び出す、 [ **WdfUsbTargetDeviceGetIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)フレームワーク ターゲットのデバイス オブジェクトに関連付けられた WDFIOTARGET ハンドルを取得します。 次に呼び出す[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) WDFIOTARGET ハンドルを指定するとします。 呼び出しでは、アクションを設定**WdfIoTargetCancelSentIo** (WDF\_IO\_ターゲット\_SENT\_IO\_アクション)。

3.  呼び出してリセット ポートの要求を送信、 [ **WdfUsbTargetDeviceResetPortSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)メソッド。

リセット ポート操作により、デバイスで USB バスで列挙を取得します。 USB ドライバー スタックは、列挙体の後にデバイスの構成を保持します。 ドライバー スタックにより、既存のパイプ ハンドルが有効であるために、クライアント ドライバーでは、以前に取得したパイプ ハンドルを使用できます。

複合デバイスの個々 の関数をリセットすることはできません。 複合デバイスでは、特定の関数のクライアント ドライバーでポートをリセット要求を送信するときに、デバイス全体がリセットされます。 USB デバイスの状態を保持する場合そのポートをリセット要求の他の関数のクライアント ドライバーに影響します。 したがって、クライアント ドライバーが、ポートをリセットする前に、パイプをリセットしようとする重要なは。

### <a href="" id="cycle-the-usb-port"></a>手順 6:USB ポートをサイクルします。

サイクル ポート操作では、電源が入っていないされ、デバイスが電気的に切断されていない点を除いて、ポートに接続されるデバイスに似ています。 デバイスが切断され、ソフトウェアで再接続されます。 この操作は、デバイスのリセットと列挙型につながります。 その結果、PnP マネージャーでは、[デバイス] ノードが再構築します。

リセット ポート操作がエラー状態をクリアしないデータ転送は引き続き失敗する場合は、サイクル ポートの要求を送信します。

1.  デバイスへのすべての転送をキャンセルします。 保留中の現在の構成で各パイプのスケジュール要求をキャンセルすることを確認します (手順 3 を参照してください)。
2.  デバイスの I/O ターゲットを停止します。

    呼び出す、 [ **WdfUsbTargetDeviceGetIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)フレームワーク ターゲットのデバイス オブジェクトに関連付けられた WDFIOTARGET ハンドルを取得します。 次に呼び出す[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) WDFIOTARGET ハンドルを指定するとします。 呼び出しでは、アクションを設定**WdfIoTargetCancelSentIo** (WDF\_IO\_ターゲット\_SENT\_IO\_アクション)。

3.  これらのメソッドのいずれかを呼び出してサイクル ポート要求を送信します。
    -   呼び出す、 [ **WdfUsbTargetDeviceCyclePortSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously)サイクル ポートの要求を同期的に送信します。
    -   呼び出す、 [ **WdfUsbTargetDeviceFormatRequestForCyclePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport)サイクル ポートの要求では、要求オブジェクトを書式設定および呼び出すことによって、要求を送信するメソッド[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。 これらの呼び出しは、手順 3. で説明したように、中止パイプ要求に似ています。

クライアント ドライバーは、サイクル ポート要求が完了した後にのみ、デバイスに転送要求を送信できます。 USB ドライバー スタック サイクル ポート要求の処理中に、[デバイス] ノードが削除されるためです。

サイクル ポート要求により、デバイスで列挙を取得します。 USB ドライバー スタックは、デバイスが切断されたことを PnP マネージャーに通知します。 PnP マネージャー クライアント ドライバーに関連付けられているデバイス スタックを廃棄します。 ドライバー スタックは、デバイスをリセット、再、USB バスでを列挙し、デバイスが接続されていることを PnP マネージャーに通知します。 PnP マネージャーでは、USB デバイスのデバイス スタックし、再構築します。

サイクルをポート操作の結果として、(この場合、アプリケーションは、このような通知の登録) を開き、デバイスにハンドルを持つ任意のアプリケーションがデバイスの削除の通知を取得します。 応答して、アプリケーションは、ユーザーにデバイス切断メッセージをレポートすることがあります。 ユーザー エクスペリエンスに影響を与える、ため、クライアント ドライバーことをお勧めサイクル ポートの要求を他の復旧メカニズムではエラー状態が解決しない場合にのみです。

同様に、リセット ポート操作 (手順 6 で説明)、複合デバイスは、サイクル ポート操作では、デバイス全体と、デバイスの個々 の機能に影響します。

## <a name="related-topics"></a>関連トピック
[USB I/O の転送](usb-device-i-o.md)  



