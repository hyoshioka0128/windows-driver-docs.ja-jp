---
title: I/O キューの移植
description: I/O キューの移植
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18fe656759e9492fbe1a2875048e7ccf5ddeb40e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390095"
---
# <a name="porting-io-queues"></a>I/O キューの移植


WDF のドライバーは、キューを作成し、I/O イベント コールバックを登録、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック。 既定では、各 I/O キュー オブジェクトは、デバイス オブジェクトの子が。 WDF ドライバーでは、キューごとに、次のタスクを構成できます。

-   どの I/O 要求の種類は、キューに送られます。
-   かどうかの要求は、(到着) としてと同時に並列にディスパッチ順番に (一度に 1 つ)、または手動で (要求時にドライバー)。
-   かどうか I/O イベント コールバック ルーチンは同時にまたは連続的に呼び出されます。
-   フレームワークまたはドライバーがシステムとデバイスの電源でキューを管理するかどうかに移行します。

キューの作成の詳細については、次を参照してください[I/O キューの作成。](creating-i-o-queues.md)

 

 





