---
title: USB パイプの使用
description: USB パイプの使用
ms.assetid: d5422ff2-de1e-4a77-8b3c-0b2917b1d9ca
keywords:
- フレームワークオブジェクト WDK KMDF、USB パイプオブジェクト
- USB パイプ WDK KMDF
- パイプオブジェクト WDK KMDF
- USB i/o ターゲット (WDK KMDF、USB パイプ)
- 継続的リーダー WDK USB
- パイプをリセットする WDK KMDF
- URBs WDK KMDF の送信
- USB 要求が WDK KMDF をブロックする
- URBs WDK KMDF
- パイプの停止 WDK KMDF
- パイプへの書き込み WDK KMDF
- パイプからの読み取り WDK KMDF
- 入力パイプ WDK KMDF
- 出力パイプ WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a2889cac9d777ea28f2daceec91b5970c9a8bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823486"
---
# <a name="working-with-usb-pipes"></a>USB パイプの使用


フレームワークは、USB インターフェイス内の各パイプをフレームワークの USB パイプオブジェクトとして表します。 ドライバーが[usb デバイスを構成](working-with-usb-devices.md#selecting-a-device-configuration)すると、フレームワークは、選択された各インターフェイスの各パイプに対してフレームワークの usb パイプオブジェクトを作成します。 パイプオブジェクトメソッドを使用すると、ドライバーは次の操作を実行できます。

-   [パイプ情報を取得します。](#obtaining-pipe-information)

-   [パイプからの読み取り。](#reading-from-a-pipe)

-   [パイプに書き込みます。](#writing-to-a-pipe)

-   [パイプを停止またはリセットします。](#stopping-and-resetting-a-pipe)

-   [パイプに URB を送信します。](#sending-a-urb-to-a-pipe)

### <a href="" id="obtaining-pipe-information"></a>パイプ情報の取得

[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)を呼び出してフレームワークの usb パイプオブジェクトへのハンドルを取得した後、ドライバーは、usb パイプに関する情報を取得するために、usb パイプオブジェクトが定義する次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipegetiotarget--------"></a>[**WdfUsbTargetPipeGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget)  
USB パイプに関連付けられている i/o ターゲットオブジェクトへのハンドルを返します。 ドライバーは、このハンドルを[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)に渡すことができます。

<a href="" id="---------wdfusbtargetpipegetinformation--------"></a>[**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)  
USB パイプとそのエンドポイントに関する情報を取得します。

<a href="" id="---------wdfusbtargetpipegettype--------"></a>[**WdfUsbTargetPipeGetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegettype)  
USB パイプの種類を返します。

<a href="" id="---------wdfusbtargetpipeisinendpoint--------"></a>[**WdfUsbTargetPipeIsInEndpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeisinendpoint)  
USB パイプが入力エンドポイントに接続されているかどうかを判断します。

<a href="" id="---------wdfusbtargetpipeisoutendpoint--------"></a>[**WdfUsbTargetPipeIsOutEndpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeisoutendpoint)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-in--------"></a>[**WDF\_USB\_パイプ\_方向\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_in)  
USB エンドポイントが入力エンドポイントであるかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-out--------"></a>[**WDF\_USB\_パイプ\_方向の\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_out)  
USB エンドポイントが出力エンドポイントであるかどうかを判断します。

関連情報については、「 [USB パイプを列挙する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)」を参照してください。

### <a href="" id="reading-from-a-pipe"></a>パイプからの読み取り

USB 入力パイプからデータを読み取るために、ドライバーは次の3つの方法のいずれか (またはすべて) を使用できます。

-   データを同期的に読み取る

    USB 入力パイプからデータを同期的に読み取るには、ドライバーで[**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)メソッドを呼び出すことができます。 このメソッドは、読み取り要求をビルドして送信し、i/o 操作が完了した後に戻ります。

-   データの非同期読み取り

    USB 入力パイプからデータを非同期に読み取るために、ドライバーは[**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)メソッドを呼び出して読み取り要求を作成できます。 次に、ドライバーは[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、要求を非同期的に (または同期的に) 送信できます。

-   データを非同期的かつ継続的に読み取る

    *継続的リーダー*は、USB パイプで読み取り要求を常に使用できるようにするためのフレームワークによって提供されるメカニズムです。 このメカニズムにより、非同期の要請されていない入力ストリームを提供するデバイスからデータを確実に受信できるようになります。 たとえば、ネットワークインターフェイスカード (NIC) のドライバーは、連続リーダーを使用して入力データを受信する場合があります。

    入力パイプの連続リーダーを構成するには、ドライバーの[*EvtdeviceWdfUsbTargetPipeConfigContinuousReader ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)メソッドを呼び出す必要があります。 このメソッドは、デバイスの i/o ターゲットに対する一連の読み取り要求をキューに置いています。

    また、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数は、 [**Wdfiotargetstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出して継続的リーダーを開始する必要があります。また、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) Callback 関数は、 [**wdfiotargetstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出して継続的に停止する必要があります。読み上げる.

    デバイスからデータが使用可能になるたびに、i/o ターゲットは読み取り要求を完了し、フレームワークは2つのコールバック関数のいずれかを呼び出します。 i/o ターゲットがデータを正常に読み取りた場合は[*EvtUsbTargetPipeReadComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_reader_completion_routine)、i/o ターゲットがエラーを報告した場合は[*EvtUsbTargetPipeReadersFailed*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed)になります。

    省略可能な[*EvtUsbTargetPipeReadersFailed*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed)コールバックを指定しない場合、フレームワークは別の読み取り要求を送信して、失敗した読み取り試行に応答します。 したがって、バスが読み取りを受け付けない状態にある場合、フレームワークは、失敗した読み取りから回復する新しい要求を継続的に送信します。

    ドライバーが[**WdfUsbTargetPipeConfigContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)を呼び出した後、ドライバーが[**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)または[**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を使用してパイプに i/o 要求を送信することはできません。ただし[ *、EvtUsbTargetPipeReadersFailed*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed) callback 関数が呼び出され、 **FALSE**を返します。

既定では、パイプの最大パケットサイズの倍数ではない読み取りバッファーがドライバーによって指定されている場合、フレームワークはエラーを報告します。 ドライバーは[**WdfUsbTargetPipeSetNoMaximumPacketSizeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesetnomaximumpacketsizecheck)を呼び出して、この読み取りバッファーサイズのテストを無効にすることができます。

関連情報については、以下を参照してください。

-   [USB 一括転送要求を送信する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [USB アイソクロナスエンドポイントにデータを転送する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [連続リーダーを使用して USB パイプからデータを読み取る方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

### <a href="" id="writing-to-a-pipe"></a>パイプへの書き込み

USB 出力パイプにデータを書き込むには、次の手法のいずれかまたは両方を使用できます。

-   データを同期的に書き込む

    データを USB 出力パイプに同期的に書き込むには、ドライバーで[**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)メソッドを呼び出すことができます。 このメソッドは、書き込み要求をビルドして送信し、i/o 操作が完了した後に戻ります。

-   データを非同期に書き込む

    データを非同期で USB 入力パイプに書き込むために、ドライバーは[**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)メソッドを呼び出して書き込み要求を作成できます。 次に、ドライバーは[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、要求を非同期的に送信できます。

関連情報については、「 [USB 一括転送要求を送信する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

### <a href="" id="stopping-and-resetting-a-pipe"></a>パイプの停止とリセット

ドライバーは、次のメソッドを呼び出して、USB パイプを停止またはリセットできます。

<a href="" id="---------wdfusbtargetpipeabortsynchronously--------"></a>[**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)  
USB パイプを停止する要求を同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforabort--------"></a>[**WdfUsbTargetPipeFormatRequestForAbort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)  
USB パイプを停止するように要求をフォーマットします。 ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、同期または非同期で要求を送信できます。

<a href="" id="---------wdfusbtargetpiperesetsynchronously--------"></a>[**WdfUsbTargetPipeResetSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)  
USB パイプをリセットする要求を同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforreset--------"></a>[**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)  
USB パイプをリセットする要求をフォーマットします。 ドライバーは、同期または非同期で要求を送信するために、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出す必要があります。

ドライバーの USB ターゲットが、エラー状態の値を含む i/o 要求を[完了](completing-i-o-requests.md)した場合、ドライバーは次のことを行う必要があります。

1.  ターゲットが要求を完了していない場合は、パイプを停止し、ドライバーが USB ターゲットに送信した追加の i/o 要求をキャンセルします。

    [**WdfIoTargetCancelSentIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action)フラグが設定された状態で[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出します。

2.  中止要求をパイプに同期的に送信します。

    [**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)を呼び出すか、 [**WdfUsbTargetPipeFormatRequestForAbort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)を呼び出した後に WDF\_\_要求で[**WDFREQUESTSEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出し、同期フラグが設定された[ **\_オプション\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)します.

3.  リセット要求をパイプに同期的に送信します。

    [**WdfUsbTargetPipeResetSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)を呼び出すか、 [**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)を呼び出した後に WDF\_\_要求で[**WDFREQUESTSEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出し、同期フラグが設定された[ **\_オプション\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)します.

4.  パイプを再起動します。

    [**Wdfiotargetstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出します。

5.  失敗した i/o 要求と、失敗した要求に続くすべての i/o 要求を再送信します。

多数の障害が発生した後、ドライバーは次の操作を行って USB ポートのリセットを試みる必要があります。

1.  すべてのアクティブなパイプを停止し、ドライバーが各パイプの USB ターゲットに送信したその他の i/o 要求を、ターゲットが完了していない場合はキャンセルします。

    アクティブなパイプごとに、 [**WdfIoTargetCancelSentIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action)フラグを設定して[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出します。

2.  USB ポートをリセットする要求を同期的に送信します。

    [**WdfUsbTargetDeviceResetPortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)を呼び出します。

3.  パイプを再起動します。

    ドライバーが停止した各パイプに対して[**Wdfiotargetstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出します。

4.  失敗した最後の i/o 要求と、失敗した要求に続くすべての i/o 要求を再送信します。

関連情報については、「 [USB パイプのエラーから回復する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)」を参照してください。

### <a href="" id="sending-a-urb-to-a-pipe"></a>パイプへの URB の送信

KMDF ドライバーが URBs を含む i/o 要求を送信して USB パイプと通信する場合、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetPipeSendUrbSynchronously (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)  
URB を含む i/o 要求を同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetPipeFormatRequestForUrb (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)  
URB を含む i/o 要求の形式を設定します。 ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、同期または非同期で要求を送信できます。

<a href="" id="---------wdfusbtargetpipewdmgetpipehandle--kmdf-only-"></a>[**WdfUsbTargetPipeWdmGetPipeHandle (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
デバイスの USBD パイプハンドルを返します。 一部の URBs では、このハンドルが必要です。

 

 





