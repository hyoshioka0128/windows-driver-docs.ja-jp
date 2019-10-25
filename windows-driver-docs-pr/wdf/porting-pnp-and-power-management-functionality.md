---
title: PnP と電源管理の移植
description: PnP と電源管理の移植
ms.assetid: 29ADD3CF-7CDE-4D97-8082-76B4F94DB6A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fc918d8e25966346db7e22529421dd78899dbc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842253"
---
# <a name="porting-pnp-and-power-management"></a>PnP と電源管理の移植


WDF は、プラグアンドプレイ (PnP) と電源管理のインテリジェントな既定値を実装しているので、単純なドライバー (ほとんどのフィルタードライバーを含む) では、PnP の基本的な要件を満たすために追加のコードは必要ありません。 このフレームワークは、PnP、電源管理、および電源ポリシーのステートマシンを自動的に作成して管理します。 既定では、次のようになります。

-   FDO は、デバイスの電源ポリシーを所有しています。
-   [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックのみが必要です。その他のすべての PnP および電源管理のコールバックは省略可能です。 ドライバーは、デバイス固有の機能をサポートするために他のコールバックを実装します。
-   フレームワークは、すべての WDFQUEUE オブジェクトの電源管理を実装します。これにより、既定の要求は、デバイスハードウェアが使用可能な場合 (つまり、D0 状態) にのみ、キューからドライバーの i/o イベントコールバックにディスパッチされます。

デバイスで割り込みやメモリの割り当てがサポートされていない場合、または電源の切り替えが発生したときに初期化または deinitialization が必要な場合、WDF ドライバーは[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックのみを必要とします。
デバイスが挿入または削除されると、フレームワークは、定義された順序で PnP および電源イベントのコールバックを呼び出します。 このセクションのトピックでは、PDOs、FDOs、およびフィルター DOs に若干異なる順序について説明します。

-   [関数またはフィルターデバイスオブジェクトの電源シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)
-   [物理デバイスオブジェクトの電源投入シーケンス](power-up-sequence-for-a-bus-driver.md)
-   [関数またはフィルターデバイスオブジェクトの電源ダウンと削除シーケンス](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [物理デバイスオブジェクトの電源ダウンと削除シーケンス](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [予期しない削除の順序](surprise-removal-sequence.md)

各マイナー PnP と電源 IRP コードに対応するコールバックの完全な一覧については、「 [WDM irp と WDF イベントコールバック関数](wdm-irps-and-kmdf-event-callback-functions.md)」を参照してください。

フレームワークベースのドライバーでの PnP および電源管理のサポートの詳細については、次のトピックを参照してください。

-   [ドライバーでの PnP と電源管理のサポート](supporting-pnp-and-power-management-in-your-driver.md)
-   [電源ポリシーの所有権](power-policy-ownership.md)

 

 





