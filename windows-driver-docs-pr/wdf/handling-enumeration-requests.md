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
ms.openlocfilehash: f6b8d03e03302621d6b0bde9d2f20cdd0fdf5a8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382849"
---
# <a name="handling-enumeration-requests"></a>列挙要求の処理


PnP マネージャーでは、いつでもその子を列挙するために、バス ドライバーを要求できます。 (列挙型の要求は、使い慣れた WDM インターフェイスを持つ場合は、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)リレーションシップの要求入力**BusRelations**)。フレームワーク ベースのドライバーでは、これらの要求は表示されません。 代わりに、フレームワークは、デバイスの子リストに格納されている情報を使用して、要求を処理します。 ドライバーは PnP マネージャーは、列挙型を要求したときに、フレームワークは正しい情報を提供できるように、子の一覧を最新に保つ責任を負います。

動的な列挙をサポートするフレームワークに基づくバス ドライバーには、特定の子デバイスを再列挙する要求を受信できます。 このような要求は、ドライバーがデバイスの障害を検出した後、子デバイスの機能のドライバーによって送信可能性があります。 (フレームワークは、実装することでこの種の要求をサポートしている、 [**再列挙\_セルフ\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reenumerate_self_interface_standard) 標準であるインターフェイス[ドライバー定義インターフェイス](using-driver-defined-interfaces.md)で定義されている*wdm.h*)。

動的な列挙をサポートするフレームワークに基づくバス ドライバーを提供できます、 [ *EvtChildListDeviceReenumerated* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_device_reenumerated)フレームワークを再列挙の受信時に、コールバック関数子デバイスのドライバーを要求します。 このコールバック関数が返す場合**TRUE**か、存在しないか、フレームワークは、子が存在するとしてマークし、PnP マネージャー、バス ドライバーの子のリストが変更されたことを通知します。 その結果、PnP マネージャーが、再列挙を要求し、フレームワークは、ドライバーの[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数は、子デバイスの新しい PDO を作成します。

 

 





