---
title: I/O キューの作成
description: I/O キューの作成
ms.assetid: 03b09c94-6b72-4234-b21f-203f93b7a2e8
keywords:
- I/o キュー WDK KMDF、作成
- I/o キュー WDK KMDF、既定値
- 既定の i/o キュー WDK KMDF
- i/o キューの作成 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dd5b886ff3c3881a16c3eaedc92a217467c8eb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841760"
---
# <a name="creating-io-queues"></a>I/O キューの作成





ほとんどのドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数に i/o キューを作成します。 デバイスの i/o キューを作成するために、ドライバーはフレームワークキューオブジェクトの[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)メソッド (フレームワークキューオブジェクトを作成) を呼び出します。 ドライバーは、 [**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体をメソッドに渡します。 この構造体には、キューの[ディスパッチメソッド](dispatching-methods-for-i-o-requests.md)や、キューで要求が使用可能になったときにフレームワークが呼び出す[要求ハンドラー](request-handlers.md)へのポインターなど、キューに関する構成情報が含まれます。 また、この構造体は、キューが[電源管理](using-power-managed-i-o-queues.md)されるかどうか、およびドライバーがキューの i/o 要求に対して長さ0のバッファーをサポートするかどうかも示します。

ドライバーによって、 [**WDF\_IO\_\_queue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)の**defaultqueue**メンバーが設定されている**場合、その**キューはデバイスの*既定の i/o キュー*になります。 ドライバーが既定の i/o キューを作成する場合、一部の要求を受信するために追加のキューを作成しない限り、フレームワークはデバイスのすべての i/o 要求をこのキューに配置します。 ドライバーは、 [**WdfDeviceGetDefaultQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)メソッドを呼び出すことによって、デバイスの既定の i/o キューへのハンドルを取得できます。

1つのデバイスに複数の i/o キューを使用する場合、ドライバーは[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して、必要な数だけキューオブジェクトを作成できます。 ドライバーが複数のキューを作成する場合、 [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出すことができます。これは、異なる種類の要求を別のキューに転送するようにフレームワークに指示します。 たとえば、すべての読み取り要求が1つのキューに配信され、すべての書き込み要求が別のキューに配信されるように指定することができます。

ドライバーが一連の i/o キューを作成し、 [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出して、ドライバーが特定のキューに対して受信できる各種類の要求をダイレクトする場合、ドライバーに既定のキューは必要ありません。

ドライバーが特定の種類の要求に対して i/o キューを提供しない場合、ドライバーが関数ドライバーの場合、フレームワークは完了状態の値\_無効\_デバイス\_要求を含むその種類の要求を完了します。 ドライバーがフィルタードライバーで、 [**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を呼び出した場合、フレームワークはこれらの要求をドライバースタック内の次の下位のドライバーに自動的に転送します。 したがって、たとえば、読み取り要求を処理しないフィルタードライバーは、読み取り要求を受信する i/o キューを提供する必要はありません。

ドライバーで i/o キューを使用する方法の例については、「 [I/o キューの使用例](example-uses-of-i-o-queues.md)」を参照してください。

 

 





