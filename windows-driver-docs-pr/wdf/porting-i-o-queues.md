---
title: I/O キューの移植
description: I/O キューの移植
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c050bb2e22959ccc263884802d1b45c6d1a0129
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379636"
---
# <a name="porting-io-queues"></a>I/O キューの移植


WDF のドライバーは、キューを作成し、I/O イベント コールバックを登録、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック。 既定では、各 I/O キュー オブジェクトは、デバイス オブジェクトの子が。 WDF ドライバーでは、キューごとに、次のタスクを構成できます。

-   どの I/O 要求の種類は、キューに送られます。
-   かどうかの要求は、(到着) としてと同時に並列にディスパッチ順番に (一度に 1 つ)、または手動で (要求時にドライバー)。
-   かどうか I/O イベント コールバック ルーチンは同時にまたは連続的に呼び出されます。
-   フレームワークまたはドライバーがシステムとデバイスの電源でキューを管理するかどうかに移行します。

キューの作成の詳細については、次を参照してください[I/O キューの作成。](creating-i-o-queues.md)

 

 





