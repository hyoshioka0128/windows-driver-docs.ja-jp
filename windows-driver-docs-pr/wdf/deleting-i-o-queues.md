---
title: I/O キューの削除
description: I/O キューの削除
ms.assetid: 7eb7a24d-de39-4e3d-865c-ebfb49d43519
keywords:
- WDK KMDF、削除の I/O キュー
- 一時的な I/O キュー WDK KMDF
- WDK KMDF キューの I/O を削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1eb3d6d35ce1cb3fe72fe4521c923b3a1ecbc3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377460"
---
# <a name="deleting-io-queues"></a>I/O キューの削除


フレームワーク ベースのドライバーには、I/O キューを作成するをいくつかのみを削除する必要があります。 ドライバーを作成する場合、[既定の I/O キュー](creating-i-o-queues.md)または呼び出すことによって構成対象 I/O キュー [ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)フレームワークは、キューを削除します。ドライバーのオブジェクトです。

たとえばの各デバイスの I/O キューの各デバイスがシステムに接続されている限りに存在する場合には、ドライバーはキューを作成、I/O でその[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 ドライバーが読み取り要求を除くすべての要求を受信する既定のキューを作成し、読み取り要求を別のキューのみを受信します。

ドライバーは、これらの I/O キューを削除できません。 代わりに、フレームワークでは、キューが所属するデバイス オブジェクトを削除するときに、キュー オブジェクトが削除されます。 ドライバーがこれらの I/O キューを削除できません理由については、次の注を参照してください。

かどうか、ただし、ドライバー、キューを作成一時 I/O 以外の[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出す必要があります[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)を使用してそれらが完了すると、これらのキューを削除します。 たとえば、提供するドライバー、 [ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数は、特定のフレームワークのファイル オブジェクトに関連付けられている I/O 要求を処理するために、I/O キューを作成可能性があります。 この場合は、ドライバーの[ *EvtFileCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)コールバック関数を呼び出す必要があります[ **WdfIoQueuePurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)キューを削除し、呼び出す**WdfObjectDelete**を削除します。

**注**  フレームワークでは、既定の I/O キュー、または特定の種類のすべての I/O 要求を受信するドライバーを構成するすべての I/O キューを削除するためのドライバーが許可されていません (呼び出して[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching))。 ドライバーを呼び出す場合[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) 、これらのキューの 1 つを表すキュー オブジェクトを削除する**WdfObjectDelete**オブジェクトを削除せずに返します。 **WdfObjectDelete**状態の戻り値を表示されないので、フレームワークがある場合にのみ、エラーを報告[フレームワークの検証ツールを使用して](using-kmdf-verifier.md)します。

 

 

 





