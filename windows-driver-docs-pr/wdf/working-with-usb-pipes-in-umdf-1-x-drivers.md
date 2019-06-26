---
title: UMDF 1.x ドライバーでの USB パイプの操作
description: UMDF 1.x ドライバーでの USB パイプの操作
ms.assetid: face26da-fa79-4d32-8ad1-9e8022bb23b3
keywords:
- UMDF WDK、USB パイプ
- ユーザー モード ドライバー フレームワーク WDK、USB パイプ
- ユーザー モード ドライバー WDK UMDF、USB パイプ
- USB パイプ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94ee95a4ee674ce77e419224444cb6a9744e19b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371740"
---
# <a name="working-with-usb-pipes-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB パイプの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、フレームワークの USB パイプ オブジェクトとして USB インターフェイスで各パイプを表します。 ドライバーは、USB デバイスを構成、するときに、フレームワークは、選択した各インターフェイスで各パイプのフレームワークの USB パイプ オブジェクトを作成します。 パイプ オブジェクトのメソッドでは、ドライバーを有効にします。

-   [パイプの情報を取得](#obtaining-umdf-usb-pipe-information)します。

-   [パイプから読み取る](#reading-from-a-umdf-usb-pipe)します。

-   [パイプに書き込む](#writing-to-a-umdf-usb-pipe)します。

-   [停止、フラッシュ、またはパイプのリセット](#stopping-flushing)します。

-   [パイプのポリシー設定](#setting-pipe-policy)します。

-   [処理のパイプ エラー](#handling-pipe-errors)します。

### <a name="obtaining-umdf-usb-pipe-information"></a>UMDF USB パイプの情報を取得します。

UMDF ドライバーを呼び出してから、 [ **IWDFUsbInterface::RetrieveUsbPipeObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)へのポインターを取得するメソッド、 [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)を USB パイプ オブジェクトのインターフェイスをドライバーは、USB パイプに関する情報を取得するため、USB パイプ オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbtargetpipe--getinformation"></a>[**IWDFUsbTargetPipe::GetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)  
USB パイプとエンドポイントに関する情報を取得します。

<a href="" id="iwdfusbtargetpipe--gettype"></a>[**IWDFUsbTargetPipe::GetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-gettype)  
USB パイプの型を返します。

<a href="" id="iwdfusbtargetpipe--isinendpoint"></a>[**IWDFUsbTargetPipe::IsInEndPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isinendpoint)  
入力エンドポイントには USB パイプが接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--isoutendpoint"></a>[**IWDFUsbTargetPipe::IsOutEndPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isoutendpoint)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--retrievepipepolicy"></a>[**IWDFUsbTargetPipe::RetrievePipePolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-retrievepipepolicy)  
WinUsb パイプのポリシーを取得します。

### <a name="reading-from-a-umdf-usb-pipe"></a>UMDF USB パイプからの読み取り

USB 入力パイプからデータを読み取るには、ドライバーは、次の手法のいずれか (または両方) を使用できます。

-   同期的にデータを読み取ります。

    UMDF ドライバーの最初の呼び出しデータを同期的に USB 入力パイプから読み取りするには、 [ **IWDFIoTarget::FormatRequestForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)読み取り要求を構築するメソッド。 ドライバーの呼び出し後、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send) 、WDF を指定して、メソッド\_要求\_送信\_オプション\_同期フラグを送信するには要求に同期的にします。

-   データを非同期的に読み取ります。

    UMDF ドライバーの最初の呼び出し USB 入力パイプからデータを非同期的に読み取りするには、 [ **IWDFIoTarget::FormatRequestForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)読み取り要求を構築するメソッド。 ドライバーの呼び出し後、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッド、WDF を指定せず\_要求\_送信\_オプション\_同期フラグ。

-   同期と継続的にデータを読み取ります。

    A*継続的なリーダー* USB パイプが常に読み取り要求に確実に framework が指定したメカニズムです。 このメカニズムは、ドライバーは、非同期、要請されていない入力ストリームを提供するデバイスからデータを受信する準備が常に保証されます。 たとえばのネットワーク インターフェイス カード (NIC) ドライバーで継続的なリーダーを使用して、入力データを受信する可能性があります。

    入力のパイプをドライバーの継続的なリーダーを構成する[ **IPnpCallbackHardware::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)コールバック関数を呼び出す必要があります、 [ **IWDFUsbTargetPipe2: ConfigureContinuousReader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)メソッド。 このメソッドは、一連のデバイスの I/O ターゲットへの読み取り要求をキューします。

    また、ドライバーの[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)コールバック関数を呼び出す必要があります[ **IWDFIoTargetStateManagement::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を開始するには継続的なリーダーとドライバーの[ **IPnpCallback::OnD0Exit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)コールバック関数を呼び出す必要があります[ **IWDFIoTargetStateManagement::Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を継続的なリーダーを停止します。

    データは、デバイスから使用するたびにでは、I/O ターゲットは、読み取り要求を完了し、フレームワークは 2 つのコールバック関数のいずれかで呼び出されます。[**IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion) I/O ターゲットは、データを正常に読み取られた場合、または[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure) I/O ターゲットは、エラーを報告する場合。

    ドライバーが呼び出された後[ **IWDFUsbTargetPipe2::ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)、ドライバーを使用できない[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)しない限り、パイプする I/O 要求を送信するドライバーの[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)コールバック関数と呼びます返します **。FALSE**します。

    継続的なリーダーは、UMDF バージョン 1.9 でサポートされている以降です。

### <a name="writing-to-a-umdf-usb-pipe"></a>UMDF USB パイプへの書き込み

USB 出力パイプにデータの書き込みに UMDF ドライバーは呼び出すことができます最初、 [ **IWDFIoTarget::FormatRequestForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)書き込み要求を構築するメソッド。 ドライバーを呼び出すことができ、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)要求を非同期的に送信するメソッド。

### <a href="" id="stopping-flushing"></a>停止、フラッシュ、および UMDF USB パイプをリセットします。

UMDF ドライバーでは、停止、フラッシュ、または USB パイプをリセットするには、次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbtargetpipe--abort"></a>[**IWDFUsbTargetPipe::Abort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort)  
USB パイプで保留中のすべての転送を停止する要求を同期的に送信します。

<a href="" id="iwdfusbtargetpipe--flush"></a>[**IWDFUsbTargetPipe::Flush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-flush)  
同期的に、デバイスには、クライアントが要求されたより多くのデータが返されるときに、WinUsb が保存されているデータを破棄する要求を送信します。

<a href="" id="iwdfusbtargetpipe--reset"></a>[**IWDFUsbTargetPipe::Reset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset)  
USB パイプにリセットする要求を同期的に送信します。

### <a href="" id="setting-pipe-policy"></a>UMDF USB パイプのポリシーの設定

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetPipe::SetPipePolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-setpipepolicy) USB パイプ (タイムアウト、パケットの短い処理、およびその他の動作など) の WinUsb によって使用される動作を制御する方法.

### <a name="handling-pipe-errors"></a>パイプ エラーの処理

場合は、ドライバーの USB ターゲット[完了](completing-i-o-requests.md)エラー状態の値を持つ、I/O 要求には、ドライバーは、次を行う必要があります。

1.  呼び出す[ **IWDFIoTargetStateManagement::Stop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)で、 **WdfIoTargetCancelSentIo**フラグを設定します。 この呼び出しは、パイプを停止し、ターゲットが、要求を完了していない場合、ドライバーが、USB ターゲットに送信する追加の I/O 要求をキャンセルします。

2.  呼び出す[ **IWDFUsbTargetPipe::Abort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort)パイプに中断要求を送信します。

3.  呼び出す[ **IWDFUsbTargetPipe::Reset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset)パイプへのリセット要求を送信します。

4.  呼び出す[ **IWDFIoTargetStateManagement::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)パイプを再起動します。

5.  失敗した場合、I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

 

 





