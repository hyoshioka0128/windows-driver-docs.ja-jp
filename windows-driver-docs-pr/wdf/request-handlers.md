---
title: 要求ハンドラー
description: 要求ハンドラー
ms.assetid: bfc543bf-18a8-4e2c-ba7a-d0a21cefb038
keywords:
- I/O キューの作成の WDK KMDF
- 要求ハンドラーの I/O キュー WDK KMDF、
- 要求ハンドラー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af70dbb2c27f1f24334d50f8099c0e8a6345664a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376277"
---
# <a name="request-handlers"></a>要求ハンドラー





順次または並列には、ドライバーが指定した場合[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)I/O キューの場合、フレームワーク、ドライバーによって提供されるコールバック関数たびに、キューの要求のいずれかをドライバーに配信する準備ができています。

ドライバーが I/O キューごとと呼ばれる次のコールバック関数の 1 つ以上提供できる*要求ハンドラー*:

<a href="" id="evtioread"></a>[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)  
フレームワークの I/O キューの[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)読み取り要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiowrite"></a>[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)  
フレームワークの I/O キューの[ *EvtIoWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)書き込み要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiodevicecontrol"></a>[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)  
フレームワークの I/O キューの[ *EvtIoDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)デバイス I/O 制御の要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiointernaldevicecontrol"></a>[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)  
フレームワークの I/O キューの[ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)デバイス I/O が内部のコントロール要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiodefault"></a>[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)  
フレームワークの I/O キューの[ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数のすべての要求が使用できるドライバーが関連付けられている要求の種類に固有のコールバック関数を提供していない場合。

呼び出すときに、ドライバーがコールバック関数を登録[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)デバイスの I/O キューを作成します。

これらのコールバック関数の 2 つの入力引数を受信します。 フレームワークは、ドライバーと、要求に保持されている I/O キューを識別するハンドルを提供する I/O 要求を識別するハンドル。 コールバック関数が呼び出すことによって、ターゲット デバイスを調べる[ **WdfIoQueueGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetdevice)します。

フレームワークは、任意のスレッド コンテキストで、ドライバーの要求ハンドラーを呼び出します。 ドライバーを任意のスレッド コンテキストで実行中に長時間待機する必要があります。 場合によってには、ドライバーは、同期メカニズムとしてカーネルのディスパッチャー オブジェクトを使用する可能性があります。 ディスパッチャー オブジェクトの場合、ドライバーが待機できる場合とできない場合の対処方法については、次を参照してください。[カーネルのディスパッチャー オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)します。

 

 





