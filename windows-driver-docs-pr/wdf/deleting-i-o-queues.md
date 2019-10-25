---
title: I/O キューの削除
description: I/O キューの削除
ms.assetid: 7eb7a24d-de39-4e3d-865c-ebfb49d43519
keywords:
- I/o キュー WDK KMDF、削除
- 一時 i/o キュー (WDK KMDF)
- i/o キューの削除 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf611c10b3d36001c76e8abffdeb809cd1fa7982
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841754"
---
# <a name="deleting-io-queues"></a>I/O キューの削除


フレームワークベースのドライバーでは、自分が作成した一部の i/o キューだけを削除する必要があります。 ドライバーが[既定の i/o キュー](creating-i-o-queues.md)または[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出すことによって構成される i/o キューを作成する場合、フレームワークはドライバーのキューオブジェクトを削除します。

たとえば、各デバイスがシステムに接続されたままである限り、各デバイスの i/o キューが存在するようにする場合、ドライバーは[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数にその i/o キューを作成します。 お使いのドライバーは、読み取り要求以外のすべての要求を受信する既定のキューと、読み取り要求のみを受信する別のキューを作成する場合があります。

ドライバーは、これらの i/o キューを削除できません。 代わりに、キューが属するデバイスオブジェクトを削除するときに、フレームワークによってキューオブジェクトが削除されます。 ドライバーがこれらの i/o キューを削除できない理由の詳細については、次のメモを参照してください。

ただし、ドライバーが[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数の外部で一時 i/o キューを作成する場合は、 [**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して、キューの使用が終了したときにこれらのキューを削除する必要があります。 たとえば、 [*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数を提供するドライバーは、特定のフレームワークファイルオブジェクトに関連付けられている i/o 要求を処理するための i/o キューを作成する場合があります。 この場合、ドライバーの[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup) callback 関数は、 [**Wdfioqueuepurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)を呼び出してキューを消去してから、 **wdfobjectdelete**を呼び出して削除する必要があります。

このフレームワークでは、ドライバーが既定の i/o キューを削除することを許可しない  、またはドライバーが特定の種類のすべての i/o 要求 ( [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出すことによって) を受信するように構成されている i/o キューを許可していない**ことに注意**してください。 ドライバーが[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して、これらのキューのいずれかを表す queue オブジェクトを削除した場合、 **wdfobjectdelete**はオブジェクトを削除せずに返します。 **Wdfobjectdelete**は戻り値の状態を提供しないため、フレームワークは、[フレームワークの検証ツールを使用して](using-kmdf-verifier.md)いる場合にのみエラーを報告します。

 

 

 





