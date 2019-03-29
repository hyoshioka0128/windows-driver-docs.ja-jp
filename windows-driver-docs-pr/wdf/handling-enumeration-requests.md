---
title: 列挙要求の処理
description: 列挙要求の処理
ms.assetid: 3719ffa7-2daf-4716-a183-531837be99aa
keywords:
- WDK KMDF 列挙型
- PnP WDK KMDF、バスの列挙型
- プラグ アンド プレイ WDK KMDF、バスの列挙型
- バスの WDK KMDF 列挙型
- WDK KMDF の子デバイスの一覧を表示します。
- WDK KMDF の子デバイス
- WDK KMDF の動的な列挙型
- 静的列挙 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7acccaf5603ad4dbcc22a3f2d4aaaa530b05fb9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571134"
---
# <a name="handling-enumeration-requests"></a>列挙要求の処理


PnP マネージャーでは、いつでもその子を列挙するために、バス ドライバーを要求できます。 (列挙型の要求は、使い慣れた WDM インターフェイスを持つ場合は、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://msdn.microsoft.com/library/windows/hardware/ff551670)リレーションシップの要求入力**BusRelations**)。フレームワーク ベースのドライバーでは、これらの要求は表示されません。 代わりに、フレームワークは、デバイスの子リストに格納されている情報を使用して、要求を処理します。 ドライバーは PnP マネージャーは、列挙型を要求したときに、フレームワークは正しい情報を提供できるように、子の一覧を最新に保つ責任を負います。

動的な列挙をサポートするフレームワークに基づくバス ドライバーには、特定の子デバイスを再列挙する要求を受信できます。 このような要求は、ドライバーがデバイスの障害を検出した後、子デバイスの機能のドライバーによって送信可能性があります。 (フレームワークは、実装することでこの種の要求をサポートしている、 [**再列挙\_セルフ\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff560839) 標準であるインターフェイス[ドライバー定義インターフェイス](using-driver-defined-interfaces.md)で定義されている*wdm.h*)。

動的な列挙をサポートするフレームワークに基づくバス ドライバーを提供できます、 [ *EvtChildListDeviceReenumerated* ](https://msdn.microsoft.com/library/windows/hardware/ff540830)フレームワークを再列挙の受信時に、コールバック関数子デバイスのドライバーを要求します。 このコールバック関数が返す場合**TRUE**か、存在しないか、フレームワークは、子が存在するとしてマークし、PnP マネージャー、バス ドライバーの子のリストが変更されたことを通知します。 その結果、PnP マネージャーが、再列挙を要求し、フレームワークは、ドライバーの[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)コールバック関数は、子デバイスの新しい PDO を作成します。

 

 





