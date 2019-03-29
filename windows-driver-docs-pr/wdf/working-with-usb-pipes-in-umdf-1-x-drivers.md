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
ms.openlocfilehash: 8a27a7841c407462bcc26581e52ef76269d57422
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572897"
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

UMDF ドライバーを呼び出してから、 [ **IWDFUsbInterface::RetrieveUsbPipeObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560339)へのポインターを取得するメソッド、 [IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)を USB パイプ オブジェクトのインターフェイスをドライバーは、USB パイプに関する情報を取得するため、USB パイプ オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbtargetpipe--getinformation"></a>[**IWDFUsbTargetPipe::GetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff560403)  
USB パイプとエンドポイントに関する情報を取得します。

<a href="" id="iwdfusbtargetpipe--gettype"></a>[**IWDFUsbTargetPipe::GetType**](https://msdn.microsoft.com/library/windows/hardware/ff560406)  
USB パイプの型を返します。

<a href="" id="iwdfusbtargetpipe--isinendpoint"></a>[**IWDFUsbTargetPipe::IsInEndPoint**](https://msdn.microsoft.com/library/windows/hardware/ff560410)  
入力エンドポイントには USB パイプが接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--isoutendpoint"></a>[**IWDFUsbTargetPipe::IsOutEndPoint**](https://msdn.microsoft.com/library/windows/hardware/ff560414)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--retrievepipepolicy"></a>[**IWDFUsbTargetPipe::RetrievePipePolicy**](https://msdn.microsoft.com/library/windows/hardware/ff560418)  
WinUsb パイプのポリシーを取得します。

### <a name="reading-from-a-umdf-usb-pipe"></a>UMDF USB パイプからの読み取り

USB 入力パイプからデータを読み取るには、ドライバーは、次の手法のいずれか (または両方) を使用できます。

-   同期的にデータを読み取ります。

    UMDF ドライバーの最初の呼び出しデータを同期的に USB 入力パイプから読み取りするには、 [ **IWDFIoTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)読み取り要求を構築するメソッド。 ドライバーの呼び出し後、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149) 、WDF を指定して、メソッド\_要求\_送信\_オプション\_同期フラグを送信するには要求に同期的にします。

-   データを非同期的に読み取ります。

    UMDF ドライバーの最初の呼び出し USB 入力パイプからデータを非同期的に読み取りするには、 [ **IWDFIoTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)読み取り要求を構築するメソッド。 ドライバーの呼び出し後、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)メソッド、WDF を指定せず\_要求\_送信\_オプション\_同期フラグ。

-   同期と継続的にデータを読み取ります。

    A*継続的なリーダー* USB パイプが常に読み取り要求に確実に framework が指定したメカニズムです。 このメカニズムは、ドライバーは、非同期、要請されていない入力ストリームを提供するデバイスからデータを受信する準備が常に保証されます。 たとえばのネットワーク インターフェイス カード (NIC) ドライバーで継続的なリーダーを使用して、入力データを受信する可能性があります。

    入力のパイプをドライバーの継続的なリーダーを構成する[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)コールバック関数を呼び出す必要があります、 [ **IWDFUsbTargetPipe2: ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)メソッド。 このメソッドは、一連のデバイスの I/O ターゲットへの読み取り要求をキューします。

    また、ドライバーの[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)コールバック関数を呼び出す必要があります[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)を開始するには継続的なリーダーとドライバーの[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)コールバック関数を呼び出す必要があります[ **IWDFIoTargetStateManagement::Stop**](https://msdn.microsoft.com/library/windows/hardware/ff559217)を継続的なリーダーを停止します。

    データは、デバイスから使用するたびにでは、I/O ターゲットは、読み取り要求を完了し、フレームワークは 2 つのコールバック関数のいずれかで呼び出されます。[**IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556910) I/O ターゲットは、データを正常に読み取られた場合、または[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915) I/O ターゲットは、エラーを報告する場合。

    ドライバーが呼び出された後[ **IWDFUsbTargetPipe2::ConfigureContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff560395)、ドライバーを使用できない[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)しない限り、パイプする I/O 要求を送信するドライバーの[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915)コールバック関数と呼びます返します **。FALSE**します。

    継続的なリーダーは、UMDF バージョン 1.9 でサポートされている以降です。

### <a name="writing-to-a-umdf-usb-pipe"></a>UMDF USB パイプへの書き込み

USB 出力パイプにデータの書き込みに UMDF ドライバーは呼び出すことができます最初、 [ **IWDFIoTarget::FormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559236)書き込み要求を構築するメソッド。 ドライバーを呼び出すことができ、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)要求を非同期的に送信するメソッド。

### <a href="" id="stopping-flushing"></a>停止、フラッシュ、および UMDF USB パイプをリセットします。

UMDF ドライバーでは、停止、フラッシュ、または USB パイプをリセットするには、次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbtargetpipe--abort"></a>[**IWDFUsbTargetPipe::Abort**](https://msdn.microsoft.com/library/windows/hardware/ff560397)  
USB パイプで保留中のすべての転送を停止する要求を同期的に送信します。

<a href="" id="iwdfusbtargetpipe--flush"></a>[**IWDFUsbTargetPipe::Flush**](https://msdn.microsoft.com/library/windows/hardware/ff560400)  
同期的に、デバイスには、クライアントが要求されたより多くのデータが返されるときに、WinUsb が保存されているデータを破棄する要求を送信します。

<a href="" id="iwdfusbtargetpipe--reset"></a>[**IWDFUsbTargetPipe::Reset**](https://msdn.microsoft.com/library/windows/hardware/ff560416)  
USB パイプにリセットする要求を同期的に送信します。

### <a href="" id="setting-pipe-policy"></a>UMDF USB パイプのポリシーの設定

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetPipe::SetPipePolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff560421) USB パイプ (タイムアウト、パケットの短い処理、およびその他の動作など) の WinUsb によって使用される動作を制御する方法.

### <a name="handling-pipe-errors"></a>パイプ エラーの処理

場合は、ドライバーの USB ターゲット[完了](completing-i-o-requests.md)エラー状態の値を持つ、I/O 要求には、ドライバーは、次を行う必要があります。

1.  呼び出す[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)で、 **WdfIoTargetCancelSentIo**フラグを設定します。 この呼び出しは、パイプを停止し、ターゲットが、要求を完了していない場合、ドライバーが、USB ターゲットに送信する追加の I/O 要求をキャンセルします。

2.  呼び出す[ **IWDFUsbTargetPipe::Abort** ](https://msdn.microsoft.com/library/windows/hardware/ff560397)パイプに中断要求を送信します。

3.  呼び出す[ **IWDFUsbTargetPipe::Reset** ](https://msdn.microsoft.com/library/windows/hardware/ff560416)パイプへのリセット要求を送信します。

4.  呼び出す[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)パイプを再起動します。

5.  失敗した場合、I/O 要求と失敗した要求の後にすべての I/O 要求を再送信します。

 

 





