---
title: I/O キューのイベント コールバック関数
description: I/O キューのイベント コールバック関数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- WDK UMDF の I/O キュー
- WDK UMDF キュー
- WDK UMDF のコールバック関数
- WDK UMDF のイベントのコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ff812fb811f538e8f100dfc5fc9218f9e23a6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382834"
---
# <a name="io-queue-event-callback-functions"></a>I/O キューのイベント コールバック関数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、の I/O キューを作成または既定の I/O キューの構成、フレームワークは、インターフェイスに関連するイベントが発生したときに、--インターフェイスに関連付けられているメソッドを呼び出すことによって、ドライバーを通知するため、次のインターフェイスを登録することができます。 I/O キューの作成と構成の I/O キューの詳細については、次を参照してください。 [Framework I/O キュー オブジェクト](framework-i-o-queue-object.md)します。

[IQueueCallbackCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackcreate)

[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)

[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackread)

[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackwrite)

[IQueueCallbackDefaultIoHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdefaultiohandler)

 

 





