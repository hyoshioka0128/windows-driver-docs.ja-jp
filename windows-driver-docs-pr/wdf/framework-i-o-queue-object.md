---
title: フレームワーク I/O キュー オブジェクト
description: フレームワーク I/O キュー オブジェクト
ms.assetid: b343c61a-8252-4e46-9013-bef29d9ec360
keywords:
- UMDF オブジェクト WDK、i/o キューオブジェクト
- フレームワークオブジェクト WDK UMDF、i/o queue オブジェクト
- I/o キューオブジェクト WDK UMDF
- IWDFIoQueue
- queue オブジェクト WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64cca126dd69a87e07b81998ad5453db0402f908
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210414"
---
# <a name="framework-io-queue-object"></a>フレームワーク I/O キュー オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークの i/o キューオブジェクトは、 [Iwdfioqueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue)インターフェイスによってドライバーに公開されます。 これは i/o キューを表します。これは、i/o 要求のコンテナーです。 I/o キューは、ドライバーへの要求のフローを制御します。 I/o 要求が到着すると、適切なキューに配置されます。 I/o キューオブジェクトは、 [UMDF デバイスオブジェクト](framework-device-object.md)の子です。 ドライバーは、 [**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを呼び出して、i/o キューオブジェクトを作成できます。 **Iwdfdevice:: CreateIoQueue**の呼び出しでは、キューが既定のキューであるかどうかをドライバーが指定できます。

ドライバーは、i/o キューを作成するときに、ドライバーへの要求の配信を制御するディスパッチモデルを指定します。 詳細については、「 [I/o キューのディスパッチモードの構成](configuring-dispatch-mode-for-an-i-o-queue.md)」を参照してください。

ドライバーが i/o キューを作成するときに、そのインターフェイスに関連するイベントが発生したときに、そのドライバーに通知するためにフレームワークが呼び出すコールバック関数のインターフェイスを提供できます。 詳細については、「 [I/o キューイベントコールバック関数](i-o-queue-event-callback-functions.md)」を参照してください。

 

 





