---
title: PnP と電源管理の移植
description: PnP と電源管理の移植
ms.assetid: 29ADD3CF-7CDE-4D97-8082-76B4F94DB6A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6daa8fa80e9608975e12d1e449fb9631e3979f98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390082"
---
# <a name="porting-pnp-and-power-management"></a>PnP と電源管理の移植


WDF にプラグ アンド プレイ (PnP) と、電源管理のインテリジェントな既定値が実装している場合 (ほとんどのフィルター ドライバーを含む)、単純なドライバーに基本的な要件を満たすために追加のコードが必要としないため PnP します。 フレームワークは自動的に作成し、PnP、電源管理、および電源ポリシーのステート マシンを管理します。 既定では。

-   FDO には、デバイスの電源ポリシーが所有しています。
-   のみ、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバックが必要です。 その他のすべての PnP や電源管理のコールバックは省略可能です。 ドライバーは、デバイスに固有の機能をサポートするその他のコールバックを実装します。
-   フレームワークが、WDFQUEUE オブジェクトのすべての電源管理を実装できるように、既定で要求にディスパッチされるキューからドライバーの I/O イベント コールバック、デバイスのハードウェアが使用可能な場合にのみ (つまり、D0 状態で)。

デバイスが場合割り込みをサポートまたはメモリをマップまたは電源の遷移が発生したときに初期化または後処理を必要と、WDF ドライバーでのみ必要な[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック。
デバイスを挿入または削除すると、フレームワークは定義された順序での PnP、電源イベント コールバックを呼び出します。 このセクションのトピックでは、Pdo、Fdo には少し異なります順序について説明し、DOs をフィルター処理します。

-   [関数またはフィルター デバイス オブジェクトの電源投入シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)
-   [物理デバイス オブジェクトの電源投入シーケンス](power-up-sequence-for-a-bus-driver.md)
-   [電源と関数、またはフィルター デバイス オブジェクトのシーケンスを削除](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [電源と物理デバイス オブジェクトのシーケンスを削除](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [シーケンスの突然の取り外し](surprise-removal-sequence.md)

各マイナー PnP と電力の IRP のコードに対応するコールバックの完全な一覧を参照してください。 [WDM Irp と WDF イベントのコールバック関数](wdm-irps-and-kmdf-event-callback-functions.md)します。

PnP をサポートしていると framework ベースのドライバーでの電源管理の詳細については、次のトピックを参照してください。

-   [ドライバーの PnP や電源管理のサポート](supporting-pnp-and-power-management-in-your-driver.md)
-   [電源ポリシーの所有権](power-policy-ownership.md)

 

 





