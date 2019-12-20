---
title: I/O キューのイベント コールバック関数
description: I/O キューのイベント コールバック関数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- I/o キュー WDK UMDF
- キュー WDK UMDF
- コールバック関数 WDK UMDF
- イベントコールバック関数 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebbd20377314e8fd703d4e138cc3fc7062b7d3f8
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209916"
---
# <a name="io-queue-event-callback-functions"></a>I/O キューのイベント コールバック関数


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーが i/o キューを作成するとき、または既定の i/o キューを構成するときに、インターフェイスに関連付けられているメソッドを呼び出すことによって、インターフェイスに関連付けられているメソッドを呼び出すことによって、フレームワークがドライバーに通知するように、次のインターフェイスを登録できます。 I/o キューの詳細および i/o キューの作成と構成の詳細については、「[フレームワーク I/o キューオブジェクト](framework-i-o-queue-object.md)」を参照してください。

[IQueueCallbackCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackcreate)

[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)

[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)

[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackwrite)

[IQueueCallbackDefaultIoHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdefaultiohandler)

 

 





