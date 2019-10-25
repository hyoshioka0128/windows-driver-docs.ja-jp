---
title: UMDF 1.x ドライバーでの USB パイプの操作
description: UMDF 1.x ドライバーでの USB パイプの操作
ms.assetid: face26da-fa79-4d32-8ad1-9e8022bb23b3
keywords:
- UMDF WDK、USB パイプ
- ユーザーモードドライバーフレームワーク WDK、USB パイプ
- ユーザーモードドライバー WDK UMDF、USB パイプ
- USB パイプ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a3ffc5b5bfae081a6e7f06e6da35a94812bbc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823499"
---
# <a name="working-with-usb-pipes-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB パイプの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、USB インターフェイス内の各パイプをフレームワークの USB パイプオブジェクトとして表します。 ドライバーが USB デバイスを構成すると、フレームワークは、選択された各インターフェイスの各パイプに対してフレームワークの USB パイプオブジェクトを作成します。 パイプオブジェクトのメソッドを使用すると、ドライバーは次のことを実行できます。

-   [パイプ情報を取得](#obtaining-umdf-usb-pipe-information)します。

-   [パイプからの読み取り](#reading-from-a-umdf-usb-pipe)。

-   [パイプに書き込み](#writing-to-a-umdf-usb-pipe)ます。

-   [パイプを停止、フラッシュ、またはリセット](#stopping-flushing)します。

-   [パイプポリシーを設定](#setting-pipe-policy)します。

-   [パイプエラーを処理](#handling-pipe-errors)します。

### <a name="obtaining-umdf-usb-pipe-information"></a>UMDF USB パイプ情報の取得

UMDF ドライバーが[**IWDFUsbInterface:: RetrieveUsbPipeObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)メソッドを呼び出して、usb パイプオブジェクトの[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)インターフェイスへのポインターを取得した後、ドライバーは、usb パイプオブジェクトで定義されている次のメソッドを呼び出すことができます。USB パイプに関する情報の取得:

<a href="" id="iwdfusbtargetpipe--getinformation"></a>[**IWDFUsbTargetPipe:: GetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)  
USB パイプとそのエンドポイントに関する情報を取得します。

<a href="" id="iwdfusbtargetpipe--gettype"></a>[**IWDFUsbTargetPipe:: GetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-gettype)  
USB パイプの種類を返します。

<a href="" id="iwdfusbtargetpipe--isinendpoint"></a>[**IWDFUsbTargetPipe::IsInEndPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isinendpoint)  
USB パイプが入力エンドポイントに接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--isoutendpoint"></a>[**IWDFUsbTargetPipe:: IsOutEndPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-isoutendpoint)  
USB パイプが出力エンドポイントに接続されているかどうかを判断します。

<a href="" id="iwdfusbtargetpipe--retrievepipepolicy"></a>[**IWDFUsbTargetPipe::RetrievePipePolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-retrievepipepolicy)  
WinUsb パイプポリシーを取得します。

### <a name="reading-from-a-umdf-usb-pipe"></a>UMDF USB パイプからの読み取り

USB 入力パイプからデータを読み取るには、次の方法のいずれか (または両方) をドライバーで使用できます。

-   データを同期的に読み取ります。

    USB 入力パイプからデータを同期的に読み取るには、まず、UMDF ドライバーは[**Iwdfiotarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)メソッドを呼び出して読み取り要求を作成します。 次に、ドライバーは[**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出し、WDF\_REQUEST\_SEND\_オプション\_同期フラグを指定して、要求を同期的に送信します。

-   データを非同期に読み取ります。

    USB 入力パイプからデータを非同期に読み取るには、まず、UMDF ドライバーが[**Iwdfiotarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)メソッドを呼び出して読み取り要求を作成します。 次に、ドライバーは WDF\_REQUEST\_SEND\_オプション\_同期フラグを指定せずに、 [**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出します。

-   データを同期的かつ継続的に読み取ります。

    *継続的リーダー*は、USB パイプで読み取り要求を常に使用できるようにするフレームワークによって提供されるメカニズムです。 このメカニズムにより、ドライバーは、非同期の要請されていない入力ストリームを提供するデバイスからデータを受信する準備が常に整っていることが保証されます。 たとえば、ネットワークインターフェイスカード (NIC) のドライバーは、連続リーダーを使用して入力データを受信する場合があります。

    入力パイプの連続リーダーを構成するには、ドライバーの[**IPnpCallbackHardware:: OnIWDFUsbTargetPipe2 ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)コールバック関数で、 [ **:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)メソッドを呼び出す必要があります。 このメソッドは、デバイスの i/o ターゲットに対する一連の読み取り要求をキューに置いています。

    また、ドライバーの[**IPnpCallback:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) callback 関数は、 [**IWDFIoTargetStateManagement:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を呼び出して継続的リーダーを開始する必要があり、ドライバーの[**IPnpCallback:: OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) callback 関数はを呼び出す[**必要があります。IWDFIoTargetStateManagement:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を実行して、継続的リーダーを停止します。

    デバイスからデータが使用可能になるたびに、i/o ターゲットは読み取り要求を完了し、フレームワークは2つのコールバック関数のいずれかを呼び出します: [**IUsbTargetPipeContinuousReaderCallbackReadComplete:: OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion) (i/o ターゲットの場合)i/o ターゲットでエラーが報告された場合、データ、または[**IUsbTargetPipeContinuousReaderCallbackReadersFailed:: OnReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)が正常に読み取られました。

    ドライバーが[**IWDFUsbTargetPipe2:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)を呼び出した後、ドライバーの IUsbTargetPipeContinuousReaderCallbackReadersFailed:: O を使用しない限り、 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)を使用してパイプに i/o 要求を送信することはできません。 [**nReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)コールバック関数が呼び出され、 **FALSE**が返されます。

    継続的リーダーは、UMDF バージョン1.9 以降でサポートされています。

### <a name="writing-to-a-umdf-usb-pipe"></a>UMDF USB パイプへの書き込み

USB 出力パイプにデータを書き込むには、まず、UMDF ドライバーが[**Iwdfiotarget:: FormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)メソッドを呼び出して書き込み要求を作成します。 次に、ドライバーは[**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出して、要求を非同期的に送信できます。

### <a href="" id="stopping-flushing"></a>UMDF USB パイプの停止、フラッシュ、およびリセット

UMDF ドライバーは、次のメソッドを呼び出して、USB パイプを停止、フラッシュ、またはリセットできます。

<a href="" id="iwdfusbtargetpipe--abort"></a>[**IWDFUsbTargetPipe:: Abort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort)  
USB パイプで保留中のすべての転送を停止する要求を同期的に送信します。

<a href="" id="iwdfusbtargetpipe--flush"></a>[**IWDFUsbTargetPipe:: Flush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-flush)  
クライアントから要求されたデータよりも多くのデータが返された場合に、WinUsb によって保存されたデータを破棄する要求を同期的に送信します。

<a href="" id="iwdfusbtargetpipe--reset"></a>[**IWDFUsbTargetPipe:: Reset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset)  
USB パイプをリセットする要求を同期的に送信します。

### <a href="" id="setting-pipe-policy"></a>UMDF USB パイプのポリシーを設定する

UMDF ドライバーは、 [**IWDFUsbTargetPipe:: SetPipePolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-setpipepolicy)メソッドを呼び出して、usb パイプ用に winusb によって使用される動作 (タイムアウト、短いパケットの処理、その他の動作など) を制御できます。

### <a name="handling-pipe-errors"></a>パイプエラーの処理

ドライバーの USB ターゲットが、エラー状態の値を含む i/o 要求を[完了](completing-i-o-requests.md)した場合、ドライバーは次のことを行う必要があります。

1.  **WdfIoTargetCancelSentIo**フラグを設定して、 [**IWDFIoTargetStateManagement:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を呼び出します。 この呼び出しは、パイプを停止し、ターゲットが要求を完了していない場合に、ドライバーが USB ターゲットに送信した追加の i/o 要求をキャンセルします。

2.  [**IWDFUsbTargetPipe:: abort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-abort)を呼び出して、中止要求をパイプに送信します。

3.  [**IWDFUsbTargetPipe:: reset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-reset)を呼び出して、パイプにリセット要求を送信します。

4.  [**IWDFIoTargetStateManagement:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を呼び出して、パイプを再起動します。

5.  失敗した i/o 要求と、失敗した要求に続くすべての i/o 要求を再送信します。

 

 





