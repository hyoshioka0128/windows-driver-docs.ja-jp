---
title: フレームワーク I/O キュー オブジェクト
description: フレームワーク I/O キュー オブジェクト
ms.assetid: b343c61a-8252-4e46-9013-bef29d9ec360
keywords:
- UMDF オブジェクト WDK、I/O の queue オブジェクトします。
- フレームワークは、WDK UMDF、I/O キューのオブジェクトをオブジェクトします。
- I/O キュー オブジェクト WDK UMDF
- IWDFIoQueue
- queue オブジェクトは WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93db224fe5a7b912130f745a2a1d49d23d73add5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373724"
---
# <a name="framework-io-queue-object"></a>フレームワーク I/O キュー オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework I/O キュー オブジェクトが、ドライバーに公開される、 [IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue)インターフェイス。 I/O 要求のコンテナーは、I/O キューを表します。 I/O キューをドライバーに要求のフローを制御します。 I/O 要求が到着するは、適切なキューに配置されます。 I/O キューのオブジェクトの子である[UMDF デバイス オブジェクト](framework-device-object.md)します。 ドライバーを呼び出すことができます、 [ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) I/O キューのオブジェクトを作成します。 呼び出しで**IWDFDevice::CreateIoQueue**ドライバーは、キューが、既定のキューであるかどうかを指定できます。

ドライバーは、I/O キューを作成するときに、ドライバーへの要求の配信を制御するディスパッチ モデルを指定します。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)します。

ドライバーは、I/O キューを作成するときに、インターフェイスに関連するイベントが発生した場合、ドライバーに通知するフレームワークから呼び出されるコールバック関数のインターフェイスを提供できます。 詳細については、次を参照してください。 [I/O キュー イベントのコールバック関数](i-o-queue-event-callback-functions.md)します。

 

 





