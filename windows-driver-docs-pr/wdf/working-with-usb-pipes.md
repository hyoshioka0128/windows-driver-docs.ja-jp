---
title: USB パイプの使用
description: USB パイプの使用
ms.assetid: d5422ff2-de1e-4a77-8b3c-0b2917b1d9ca
keywords:
- フレームワークは、WDK KMDF、USB パイプ オブジェクトをオブジェクトします。
- USB は、WDK KMDF、パイプを使用します。
- パイプ オブジェクト WDK KMDF
- USB I/O ターゲット WDK KMDF、USB パイプ
- 継続的なリーダー WDK USB
- パイプ WDK KMDF をリセットします。
- 翻訳の WDK KMDF を送信します。
- USB 要求 WDK KMDF をブロックします。
- 翻訳の WDK KMDF
- パイプ WDK KMDF を停止しています
- WDK KMDF パイプへの書き込み
- WDK KMDF パイプからの読み取り
- 入力パイプ WDK KMDF
- パイプ WDK KMDF を出力します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d04db4aed0658def761326c5c7ad47b7a378537a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384435"
---
# <a name="working-with-usb-pipes"></a>USB パイプの使用


フレームワークは、フレームワークの USB パイプ オブジェクトとして USB インターフェイスで各パイプを表します。 ときに、ドライバー [USB デバイスを構成します。](working-with-usb-devices.md#selecting-a-device-configuration)、フレームワークは、選択した各インターフェイスで各パイプの framework USB パイプ オブジェクトを作成します。 パイプ オブジェクトのメソッドは、次の操作を実行するためのドライバーを有効にします。

-   [パイプの情報を取得します。](#obtaining-pipe-information)

-   [パイプから読み取る。](#reading-from-a-pipe)

-   [パイプに書き込みます。](#writing-to-a-pipe)

-   [停止またはパイプをリセットします。](#stopping-and-resetting-a-pipe)

-   [パイプを URB を送信します。](#sending-a-urb-to-a-pipe)

### <a href="" id="obtaining-pipe-information"></a> パイプの情報を取得します。

呼び出した後[ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe) framework USB パイプ オブジェクトへのハンドルを取得するには、ドライバーは、取得するため、USB パイプ オブジェクトを定義する次のメソッドを呼び出すことができますUSB パイプに関する情報:

<a href="" id="---------wdfusbtargetpipegetiotarget--------"></a>[**WdfUsbTargetPipeGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget)  
USB パイプに関連付けられている I/O ターゲット オブジェクトにハンドルを返します。 ドライバーはこのハンドルを渡すことができます[ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)します。

<a href="" id="---------wdfusbtargetpipegetinformation--------"></a>[**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)  
USB パイプとエンドポイントに関する情報を取得します。

<a href="" id="---------wdfusbtargetpipegettype--------"></a>[**WdfUsbTargetPipeGetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegettype)  
USB パイプの型を返します。

<a href="" id="---------wdfusbtargetpipeisinendpoint--------"></a>[**WdfUsbTargetPipeIsInEndpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeisinendpoint)  
入力エンドポイントには USB パイプが接続されているかどうかを判断します。

<a href="" id="---------wdfusbtargetpipeisoutendpoint--------"></a>[**WdfUsbTargetPipeIsOutEndpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeisoutendpoint)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-in--------"></a>[**WDF\_USB\_パイプ\_方向\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_in)  
USB エンドポイントは入力エンドポイントであるかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-out--------"></a>[**WDF\_USB\_パイプ\_方向\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_out)  
USB エンドポイントが、出力エンドポイントであるかどうかを判断します。

関連情報については、次を参照してください。 [USB パイプを列挙する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)します。

### <a href="" id="reading-from-a-pipe"></a> パイプからの読み取り

USB 入力パイプからデータを読み取るには、ドライバーは、次の 3 つの手法のいずれか (またはすべて) を使用できます。

-   同期的にデータを読み取る

    USB 入力パイプからは同期的にデータを読み取るには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeReadSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)メソッド。 このメソッドのビルドと送信され、読み取り要求を I/O 操作が完了した後を返します。

-   非同期的にデータを読み取る

    USB 入力パイプから非同期的にデータを読み取るには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeFormatRequestForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)読み取り要求を構築するメソッド。 ドライバーを呼び出すことができますし、 [ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)非同期的に (または同期的に) 要求を送信します。

-   非同期的にかつ継続的にデータを読み取る

    A*継続的なリーダー*フレームワークが指定した読み取り要求が USB パイプを使用可能な常にあることを確認するメカニズムです。 このメカニズムでは、ドライバーが非同期の要請されていない入力ストリームを提供するデバイスからデータを受信する準備が常にすることが保証されます。 たとえばのネットワーク インターフェイス カード (NIC) ドライバーで継続的なリーダーを使用して、入力データを受信する可能性があります。

    入力のパイプをドライバーの継続的なリーダーを構成する[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を呼び出す必要があります、 [ **WdfUsbTargetPipeConfigContinuousReader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)メソッド。 このメソッドは、一連のデバイスの I/O ターゲットへの読み取り要求をキューします。

    また、ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数を呼び出す必要があります[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)連続リーダーを開始して、ドライバーの[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数を呼び出す必要があります[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を継続的なリーダーを停止します。

    データは、デバイスから使用するたびにでは、I/O ターゲットは、読み取り要求を完了し、フレームワークは 2 つのコールバック関数のいずれかで呼び出されます。[*EvtUsbTargetPipeReadComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nc-wdfusb-evt_wdf_usb_reader_completion_routine)I/O ターゲットは、データを正常に読み取られた場合、または[ *EvtUsbTargetPipeReadersFailed*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed)I/O ターゲットがエラーを報告する場合は、します。

    省略可能な指定しない場合[ *EvtUsbTargetPipeReadersFailed* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed)コールバック フレームワーク読み取り操作の失敗をもう 1 つの読み取り要求を送信することが応答します。 したがって、バスが、その読み取りを受け付けていません状態にある場合、フレームワークは継続的に失敗した読み取りから回復する新しい要求を送信します。

    ドライバーが呼び出された後[ **WdfUsbTargetPipeConfigContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)、ドライバーを使用できない[ **WdfUsbTargetPipeReadSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)または[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)しない限り、パイプする I/O 要求を送信するドライバーの[ *EvtUsbTargetPipeReadersFailed* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed)コールバック関数は呼び出され、返します**FALSE**します。

既定では、フレームワークは、ドライバーが、パイプの最大パケット サイズの倍数でない読み取りバッファーを指定する場合にエラーを報告します。 ドライバーを呼び出すことができます[ **WdfUsbTargetPipeSetNoMaximumPacketSizeCheck** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipesetnomaximumpacketsizecheck)読み取りバッファーのサイズには、このテストを無効にします。

関連情報については、次を参照してください。

-   [USB 一括転送要求を送信する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [USB アイソクロナス エンドポイントにデータを転送する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [USB パイプからデータを読み取るための継続的なリーダーを使用する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

### <a href="" id="writing-to-a-pipe"></a> パイプへの書き込み

USB 出力パイプにデータを記述するには、ドライバーは、次の手法の 1 つ (または両方) を使用できます。

-   データを同期的に書き込む

    USB 出力パイプに同期的にデータを記述するには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeWriteSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)メソッド。 このメソッドのビルドと送信書き込み要求、また、I/O 操作が完了した後を返します。

-   データを非同期的に書き込む

    USB 入力パイプにデータを非同期的に書き込みするには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeFormatRequestForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)書き込み要求を構築するメソッド。 ドライバーを呼び出すことができますし、 [ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)要求を非同期的に送信します。

関連情報については、次を参照してください。 [USB 一括転送要求を送信する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

### <a href="" id="stopping-and-resetting-a-pipe"></a> 停止して、パイプのリセット

ドライバーは、停止、または USB パイプをリセットするのには、次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipeabortsynchronously--------"></a>[**WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)  
USB パイプの停止要求が同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforabort--------"></a>[**WdfUsbTargetPipeFormatRequestForAbort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)  
USB パイプの停止要求を書式設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)同期または非同期要求を送信します。

<a href="" id="---------wdfusbtargetpiperesetsynchronously--------"></a>[**WdfUsbTargetPipeResetSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)  
USB パイプにリセットする要求を同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforreset--------"></a>[**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)  
USB パイプをリセットする要求を書式設定します。 ドライバーを呼び出す必要があります[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)同期または非同期要求を送信します。

場合は、ドライバーの USB ターゲット[完了](completing-i-o-requests.md)エラー状態の値を持つ、I/O 要求には、ドライバーは、次を行う必要があります。

1.  パイプを停止し、ターゲットが、要求を完了していない場合、ドライバーが、USB ターゲットに送信する追加の I/O 要求をキャンセルします。

    呼び出す[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)で、 [ **WdfIoTargetCancelSentIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action)フラグを設定します。

2.  パイプに中断要求が同期的に送信します。

    呼び出す[ **WdfUsbTargetPipeAbortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)、呼び出したり[ **WdfUsbTargetPipeFormatRequestForAbort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort) 続けて[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)で、 [ **WDF\_要求\_送信\_オプション\_同期**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)フラグを設定します。

3.  同期的に、パイプへのリセット要求を送信します。

    呼び出す[ **WdfUsbTargetPipeResetSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)、呼び出したり[ **WdfUsbTargetPipeFormatRequestForReset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset) 続けて[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)で、 [ **WDF\_要求\_送信\_オプション\_同期**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)フラグを設定します。

4.  パイプを再起動します。

    呼び出す[ **WdfIoTargetStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)します。

5.  失敗した場合、I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

多数の複数のエラーでは、後に、ドライバーが次の手順に従って、USB ポートをリセットしようとする必要があります。

1.  すべてのアクティブなパイプを停止し、ターゲットが完了していない場合、ドライバーが各パイプの USB のターゲットに送信する追加の I/O 要求をキャンセルします。

    アクティブな各パイプでは、呼び出す[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)で、 [ **WdfIoTargetCancelSentIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action)フラグを設定します。

2.  同期的に、USB ポートにリセットする要求を送信します。

    呼び出す[ **WdfUsbTargetDeviceResetPortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)します。

3.  パイプを再起動します。

    呼び出す[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)ドライバーが停止している各パイプの。

4.  失敗した最後の I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

関連情報については、次を参照してください。 [USB パイプ エラーから回復する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)します。

### <a href="" id="sending-a-urb-to-a-pipe"></a> パイプを URB を送信します。

翻訳が含まれている I/O 要求を送信することによって、KMDF ドライバーの USB パイプが通信する場合、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetPipeSendUrbSynchronously (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)  
同期的に、URB を含む I/O 要求を送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetPipeFormatRequestForUrb (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)  
含む、URB I/O 要求の書式を設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)同期または非同期要求を送信します。

<a href="" id="---------wdfusbtargetpipewdmgetpipehandle--kmdf-only-"></a>[**WdfUsbTargetPipeWdmGetPipeHandle (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
デバイスの USBD パイプ ハンドルを返します。 いくつかの翻訳では、このハンドルが必要です。

 

 





