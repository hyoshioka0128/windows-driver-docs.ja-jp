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
ms.openlocfilehash: 4f54a3ae3c4b4f8840a189f0cbebfe418673058e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361958"
---
# <a name="working-with-usb-pipes"></a>USB パイプの使用


フレームワークは、フレームワークの USB パイプ オブジェクトとして USB インターフェイスで各パイプを表します。 ときに、ドライバー [USB デバイスを構成します。](working-with-usb-devices.md#selecting-a-device-configuration)、フレームワークは、選択した各インターフェイスで各パイプの framework USB パイプ オブジェクトを作成します。 パイプ オブジェクトのメソッドは、次の操作を実行するためのドライバーを有効にします。

-   [パイプの情報を取得します。](#obtaining-pipe-information)

-   [パイプから読み取る。](#reading-from-a-pipe)

-   [パイプに書き込みます。](#writing-to-a-pipe)

-   [停止またはパイプをリセットします。](#stopping-and-resetting-a-pipe)

-   [パイプを URB を送信します。](#sending-a-urb-to-a-pipe)

### <a href="" id="obtaining-pipe-information"></a> パイプの情報を取得します。

呼び出した後[ **WdfUsbInterfaceGetConfiguredPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff550057) framework USB パイプ オブジェクトへのハンドルを取得するには、ドライバーは、取得するため、USB パイプ オブジェクトを定義する次のメソッドを呼び出すことができますUSB パイプに関する情報:

<a href="" id="---------wdfusbtargetpipegetiotarget--------"></a>[**WdfUsbTargetPipeGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff551146)  
USB パイプに関連付けられている I/O ターゲット オブジェクトにハンドルを返します。 ドライバーはこのハンドルを渡すことができます[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)します。

<a href="" id="---------wdfusbtargetpipegetinformation--------"></a>[**WdfUsbTargetPipeGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff551142)  
USB パイプとエンドポイントに関する情報を取得します。

<a href="" id="---------wdfusbtargetpipegettype--------"></a>[**WdfUsbTargetPipeGetType**](https://msdn.microsoft.com/library/windows/hardware/ff551148)  
USB パイプの型を返します。

<a href="" id="---------wdfusbtargetpipeisinendpoint--------"></a>[**WdfUsbTargetPipeIsInEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551151)  
入力エンドポイントには USB パイプが接続されているかどうかを判断します。

<a href="" id="---------wdfusbtargetpipeisoutendpoint--------"></a>[**WdfUsbTargetPipeIsOutEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551153)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-in--------"></a>[**WDF\_USB\_パイプ\_方向\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553027)  
USB エンドポイントは入力エンドポイントであるかどうかを判断します。

<a href="" id="---------wdf-usb-pipe-direction-out--------"></a>[**WDF\_USB\_パイプ\_方向\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553032)  
USB エンドポイントが、出力エンドポイントであるかどうかを判断します。

関連情報については、次を参照してください。 [USB パイプを列挙する方法](https://msdn.microsoft.com/library/windows/hardware/hh968306)します。

### <a href="" id="reading-from-a-pipe"></a> パイプからの読み取り

USB 入力パイプからデータを読み取るには、ドライバーは、次の 3 つの手法のいずれか (またはすべて) を使用できます。

-   同期的にデータを読み取る

    USB 入力パイプからは同期的にデータを読み取るには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155)メソッド。 このメソッドのビルドと送信され、読み取り要求を I/O 操作が完了した後を返します。

-   非同期的にデータを読み取る

    USB 入力パイプから非同期的にデータを読み取るには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff551136)読み取り要求を構築するメソッド。 ドライバーを呼び出すことができますし、 [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)非同期的に (または同期的に) 要求を送信します。

-   非同期的にかつ継続的にデータを読み取る

    A*継続的なリーダー*フレームワークが指定した読み取り要求が USB パイプを使用可能な常にあることを確認するメカニズムです。 このメカニズムでは、ドライバーが非同期の要請されていない入力ストリームを提供するデバイスからデータを受信する準備が常にすることが保証されます。 たとえばのネットワーク インターフェイス カード (NIC) ドライバーで継続的なリーダーを使用して、入力データを受信する可能性があります。

    入力のパイプをドライバーの継続的なリーダーを構成する[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数を呼び出す必要があります、 [ **WdfUsbTargetPipeConfigContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551130)メソッド。 このメソッドは、一連のデバイスの I/O ターゲットへの読み取り要求をキューします。

    また、ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数を呼び出す必要があります[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)連続リーダーを開始して、ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック関数を呼び出す必要があります[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)を継続的なリーダーを停止します。

    データは、デバイスから使用するたびにでは、I/O ターゲットは、読み取り要求を完了し、フレームワークは 2 つのコールバック関数のいずれかで呼び出されます。[*EvtUsbTargetPipeReadComplete*](https://msdn.microsoft.com/library/windows/hardware/ff541826)I/O ターゲットは、データを正常に読み取られた場合、または[ *EvtUsbTargetPipeReadersFailed*](https://msdn.microsoft.com/library/windows/hardware/ff541832)I/O ターゲットがエラーを報告する場合は、します。

    省略可能な指定しない場合[ *EvtUsbTargetPipeReadersFailed* ](https://msdn.microsoft.com/library/windows/hardware/ff541832)コールバック フレームワーク読み取り操作の失敗をもう 1 つの読み取り要求を送信することが応答します。 したがって、バスが、その読み取りを受け付けていません状態にある場合、フレームワークは継続的に失敗した読み取りから回復する新しい要求を送信します。

    ドライバーが呼び出された後[ **WdfUsbTargetPipeConfigContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff551130)、ドライバーを使用できない[ **WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155)または[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)しない限り、パイプする I/O 要求を送信するドライバーの[ *EvtUsbTargetPipeReadersFailed* ](https://msdn.microsoft.com/library/windows/hardware/ff541832)コールバック関数は呼び出され、返します**FALSE**します。

既定では、フレームワークは、ドライバーが、パイプの最大パケット サイズの倍数でない読み取りバッファーを指定する場合にエラーを報告します。 ドライバーを呼び出すことができます[ **WdfUsbTargetPipeSetNoMaximumPacketSizeCheck** ](https://msdn.microsoft.com/library/windows/hardware/ff551160)読み取りバッファーのサイズには、このテストを無効にします。

関連情報については、次を参照してください。

-   [USB 一括転送要求を送信する方法](https://msdn.microsoft.com/library/windows/hardware/ff539199)
-   [USB アイソクロナス エンドポイントにデータを転送する方法](https://msdn.microsoft.com/library/windows/hardware/hh406225)
-   [USB パイプからデータを読み取るための継続的なリーダーを使用する方法](https://msdn.microsoft.com/library/windows/hardware/hh968308)

### <a href="" id="writing-to-a-pipe"></a> パイプへの書き込み

USB 出力パイプにデータを記述するには、ドライバーは、次の手法の 1 つ (または両方) を使用できます。

-   データを同期的に書き込む

    USB 出力パイプに同期的にデータを記述するには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551163)メソッド。 このメソッドのビルドと送信書き込み要求、また、I/O 操作が完了した後を返します。

-   データを非同期的に書き込む

    USB 入力パイプにデータを非同期的に書き込みするには、ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeFormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff551141)書き込み要求を構築するメソッド。 ドライバーを呼び出すことができますし、 [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)要求を非同期的に送信します。

関連情報については、次を参照してください。 [USB 一括転送要求を送信する方法](https://msdn.microsoft.com/library/windows/hardware/ff539199)します。

### <a href="" id="stopping-and-resetting-a-pipe"></a> 停止して、パイプのリセット

ドライバーは、停止、または USB パイプをリセットするのには、次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipeabortsynchronously--------"></a>[**WdfUsbTargetPipeAbortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551129)  
USB パイプの停止要求が同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforabort--------"></a>[**WdfUsbTargetPipeFormatRequestForAbort**](https://msdn.microsoft.com/library/windows/hardware/ff551132)  
USB パイプの停止要求を書式設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

<a href="" id="---------wdfusbtargetpiperesetsynchronously--------"></a>[**WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)  
USB パイプにリセットする要求を同期的に送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforreset--------"></a>[**WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138)  
USB パイプをリセットする要求を書式設定します。 ドライバーを呼び出す必要があります[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

場合は、ドライバーの USB ターゲット[完了](completing-i-o-requests.md)エラー状態の値を持つ、I/O 要求には、ドライバーは、次を行う必要があります。

1.  パイプを停止し、ターゲットが、要求を完了していない場合、ドライバーが、USB ターゲットに送信する追加の I/O 要求をキャンセルします。

    呼び出す[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)で、 [ **WdfIoTargetCancelSentIo** ](https://msdn.microsoft.com/library/windows/hardware/ff552388)フラグを設定します。

2.  パイプに中断要求が同期的に送信します。

    呼び出す[ **WdfUsbTargetPipeAbortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551129)、呼び出したり[ **WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132) 続けて[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)で、 [ **WDF\_要求\_送信\_オプション\_同期**](https://msdn.microsoft.com/library/windows/hardware/ff552491)フラグを設定します。

3.  同期的に、パイプへのリセット要求を送信します。

    呼び出す[ **WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)、呼び出したり[ **WdfUsbTargetPipeFormatRequestForReset** ](https://msdn.microsoft.com/library/windows/hardware/ff551138) 続けて[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)で、 [ **WDF\_要求\_送信\_オプション\_同期**](https://msdn.microsoft.com/library/windows/hardware/ff552491)フラグを設定します。

4.  パイプを再起動します。

    呼び出す[ **WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)します。

5.  失敗した場合、I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

多数の複数のエラーでは、後に、ドライバーが次の手順に従って、USB ポートをリセットしようとする必要があります。

1.  すべてのアクティブなパイプを停止し、ターゲットが完了していない場合、ドライバーが各パイプの USB のターゲットに送信する追加の I/O 要求をキャンセルします。

    アクティブな各パイプでは、呼び出す[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)で、 [ **WdfIoTargetCancelSentIo** ](https://msdn.microsoft.com/library/windows/hardware/ff552388)フラグを設定します。

2.  同期的に、USB ポートにリセットする要求を送信します。

    呼び出す[ **WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)します。

3.  パイプを再起動します。

    呼び出す[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)ドライバーが停止している各パイプの。

4.  失敗した最後の I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

関連情報については、次を参照してください。 [USB パイプ エラーから回復する方法](https://msdn.microsoft.com/library/windows/hardware/hh968307)します。

### <a href="" id="sending-a-urb-to-a-pipe"></a> パイプを URB を送信します。

翻訳が含まれている I/O 要求を送信することによって、KMDF ドライバーの USB パイプが通信する場合、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetpipesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetPipeSendUrbSynchronously (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff551158)  
同期的に、URB を含む I/O 要求を送信します。

<a href="" id="---------wdfusbtargetpipeformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetPipeFormatRequestForUrb (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff551139)  
含む、URB I/O 要求の書式を設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

<a href="" id="---------wdfusbtargetpipewdmgetpipehandle--kmdf-only-"></a>[**WdfUsbTargetPipeWdmGetPipeHandle (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff551162)  
デバイスの USBD パイプ ハンドルを返します。 いくつかの翻訳では、このハンドルが必要です。

 

 





