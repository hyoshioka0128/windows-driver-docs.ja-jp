---
title: I/O キューの作成
description: I/O キューの作成
ms.assetid: 03b09c94-6b72-4234-b21f-203f93b7a2e8
keywords:
- I/O キューの作成の WDK KMDF
- WDK KMDF、既定の I/O キュー
- 既定の I/O キュー WDK KMDF
- WDK KMDF キューの I/O を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 679be0780c0564f58c23797846cb73f59a074a1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382370"
---
# <a name="creating-io-queues"></a>I/O キューの作成





ほとんどのドライバーでの I/O キューの作成、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 ドライバーをデバイスの I/O キューを作成するには、するには、呼び出しのフレームワークのキュー オブジェクトの[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)メソッド (これは、framework のキュー オブジェクトが作成されます)。 ドライバーの提供、 [ **WDF\_IO\_キュー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)メソッドに構造体。 この構造体には、キューのなど、キューに関する構成情報が含まれています[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)へのポインターと[要求ハンドラー](request-handlers.md)要求をで使用可能なときにフレームワーク。キューです。 構造体もキューが必要かどうかを示す[電源管理対象](using-power-managed-i-o-queues.md)とキューの I/O 要求に、ドライバーが長さ 0 のバッファーをサポートするかどうか。

ドライバーが設定されている場合、 **DefaultQueue**のメンバー、 [ **WDF\_IO\_キュー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)構造体を**TRUE**、キューが、デバイスの*既定の I/O キュー*します。 ドライバーは、既定の I/O キューを作成する場合、フレームワークすべてのデバイスの I/O 要求キューに配置この、一部の要求を受信するキューを作成しない限り、します。 ドライバーは呼び出すことによって、デバイスの既定の I/O キューを識別するハンドルを取得することができます、 [ **WdfDeviceGetDefaultQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)メソッド。

デバイスは、複数の I/O キューを使用する場合、ドライバーを呼び出すことができます[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)必要がある多くの queue オブジェクトを作成します。 呼び出すことができる場合、ドライバーは、複数のキューを作成、 [ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)、さまざまな種類の別のキューに要求を送信するためにフレームワークを指示します。 たとえば、要求が 1 つのキューに配信され、すべての書き込み要求は別のキューに配信をすべて読み取ることを指定できます。

ドライバーが呼び出しや I/O キューのセットを作成するかどうかは[ **WdfDeviceConfigureRequestDispatching** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)ドライバーは、特定のキューに受け取ることができる要求の種類ごとに、ドライバーは必要はありません、既定のキュー。

ドライバーは、特定の種類の要求を I/O キューを提供しませんし、フレームワークがステータスの完了状態の値をその型の要求を完了すると、ドライバーが関数のドライバーの場合は場合、\_無効な\_デバイス\_要求します。 ドライバーをフィルター ドライバーが呼び出されていて[ **WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)フレームワークは、次の下位ドライバーはドライバー スタックにこれらの要求を自動的に転送します。 そのため、たとえば、フィルター ドライバーは処理されませんの読み取り要求が読み取り要求を受信する I/O キューを提供する必要はありません。

ドライバーが I/O キューを使用する方法の例については、次を参照してください。 [I/O キューの使用例を使用して](example-uses-of-i-o-queues.md)します。

 

 





