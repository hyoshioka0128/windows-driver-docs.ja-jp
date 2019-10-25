---
title: 列挙要求の処理
description: 列挙要求の処理
ms.assetid: 3719ffa7-2daf-4716-a183-531837be99aa
keywords:
- 列挙型 WDK KMDF
- PnP WDK KMDF、bus 列挙型
- プラグアンドプレイ WDK KMDF、bus 列挙型
- バス列挙型 WDK KMDF
- 子デバイスの一覧表示 (WDK KMDF)
- 子デバイス WDK KMDF
- 動的列挙型 WDK KMDF
- 静的な列挙型 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3f54b1da4c28cf7b78b36c15b977ab1ea0d7cd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844780"
---
# <a name="handling-enumeration-requests"></a>列挙要求の処理


PnP マネージャーは、いつでもその子を列挙するようにバスドライバーに要求できます。 (WDM インターフェイスに精通している場合、列挙要求は IRP\_によって[ **\_クエリ\_デバイス\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)関係の種類が**BUSRELATIONS**であるリレーションシップ要求) です。フレームワークベースのドライバーでは、これらの要求は表示されません。 代わりに、フレームワークは、デバイスの子リストに格納されている情報を使用して要求を処理します。 ドライバーは、子リストを最新の状態に保ち、PnP マネージャーが列挙を要求したときにフレームワークが正しい情報を提供できるようにします。

動的列挙をサポートするフレームワークベースのバスドライバーは、特定の子デバイスを reenumerate するための要求を受け取ることができます。 このような要求は、ドライバーがデバイスの障害を検出した後で、子デバイスの関数ドライバーによって送信されることがあります。 (フレームワークは、 [**REENUMERATE\_SELF\_interface\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reenumerate_self_interface_standard)インターフェイスを実装することによって、この種類の要求をサポートします。これは、 *wdm*で定義されている標準の[ドライバー定義インターフェイス](using-driver-defined-interfaces.md)です)。

動的列挙をサポートするフレームワークベースのバスドライバーは、 [*Evtchildlistdevicereenumerated*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_device_reenumerated)コールバック関数を提供できます。この関数は、子デバイスのドライバーから reenumeration 要求を受け取ったときにフレームワークによって呼び出されます。 このコールバック関数が**TRUE**を返した場合、または存在しない場合、フレームワークは子デバイスを存在しないとマークし、バスドライバーの子リストが変更されたことを PnP マネージャーに通知します。 その結果、PnP マネージャーは reenumeration を要求し、フレームワークはドライバーの[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) callback 関数を呼び出します。これにより、子デバイス用の新しい PDO が作成されます。

 

 





