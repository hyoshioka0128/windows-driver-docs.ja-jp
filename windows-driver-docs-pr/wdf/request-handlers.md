---
title: 要求ハンドラー
description: 要求ハンドラー
ms.assetid: bfc543bf-18a8-4e2c-ba7a-d0a21cefb038
keywords:
- I/o キュー WDK KMDF、作成
- I/o キュー WDK KMDF、要求ハンドラー
- 要求ハンドラー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54471c6d50ba503dec9ddfa28ee8d466e05de4f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842215"
---
# <a name="request-handlers"></a>要求ハンドラー





ドライバーで i/o キューに対して順次または並列[ディスパッチメソッド](dispatching-methods-for-i-o-requests.md)が指定されている場合、このフレームワークは、キューの要求の1つをドライバーに配信する準備が整うたびに、ドライバーによって提供されるコールバック関数を呼び出します。

ドライバーは、各 i/o キューに対して、*要求ハンドラー*と呼ばれる次のコールバック関数を1つ以上提供できます。

<a href="" id="evtioread"></a>[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)  
このフレームワークは、キューで読み取り要求が使用可能になったときに、i/o キューの[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) callback 関数を呼び出します。

<a href="" id="evtiowrite"></a>[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)  
このフレームワークは、書き込み要求がキューで利用可能な場合に、i/o キューの[*Evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)コールバック関数を呼び出します。

<a href="" id="evtiodevicecontrol"></a>[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)  
このフレームワークは、デバイス i/o 制御要求がキューで利用可能な場合に、i/o キューの[*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)コールバック関数を呼び出します。

<a href="" id="evtiointernaldevicecontrol"></a>[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)  
このフレームワークは、内部デバイスの i/o 制御要求がキューで利用可能な場合に、i/o キューの[*Evtiointernaldevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバック関数を呼び出します。

<a href="" id="evtiodefault"></a>[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)  
このフレームワークは、任意の要求が使用可能な場合に、関連付けられている要求タイプ固有のコールバック関数を提供していない場合、i/o キューの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数を呼び出します。

ドライバーは、 [**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出してデバイスの i/o キューを作成するときに、コールバック関数を登録します。

これらの各コールバック関数は、2つの入力引数を受け取ります。これは、フレームワークがドライバーに提供する i/o 要求へのハンドルと、要求を保持した i/o キューへのハンドルです。 コールバック関数は、 [**Wdfioqueuegetdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetdevice)を呼び出してターゲットデバイスを特定できます。

フレームワークは、任意のスレッドコンテキストでドライバーの要求ハンドラーを呼び出します。 ドライバーは、任意のスレッドコンテキストで実行されている間、長時間待機することはできません。 場合によっては、ドライバーがカーネルディスパッチャーオブジェクトを同期メカニズムとして使用することがあります。 ドライバーが dispatcher オブジェクトを待機できるタイミングと、できない場合の対処方法については、「[カーネルディスパッチャーオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)」を参照してください。

 

 





