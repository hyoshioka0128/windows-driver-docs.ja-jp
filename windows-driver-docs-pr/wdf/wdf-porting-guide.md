---
title: WDM から WDF へのドライバーの移植
description: このセクションのトピックでは、既存の WDM ドライバーをカーネルモードドライバーフレームワーク (KMDF) ドライバーまたはユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーに変換する方法について説明します。
ms.assetid: 3B4D677D-2FCC-45A1-95B4-DA9CA9D7B452
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a07228b1f5d56061f319fd7736f11577c40e72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845415"
---
# <a name="porting-a-driver-from-wdm-to-wdf"></a>WDM から WDF へのドライバーの移植


このセクションのトピックでは、既存の WDM ドライバーをカーネルモードドライバーフレームワーク (KMDF) ドライバーまたはユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーに変換する方法について説明します。

アーキテクチャ上、Windows ドライバーフレームワーク (WDF) ドライバーは、WDM ドライバーに似ています。 WDM ドライバーは、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数、オペレーティングシステムによってサービス i/o 要求が呼び出されるさまざまなディスパッチルーチン、およびドライバー固有のその他のユーティリティ関数で構成されています。 WDF ドライバーは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数、フレームワークがサービス i/o 要求を呼び出すさまざまなイベントコールバック関数、およびドライバー固有のその他のユーティリティ関数で構成されています。 ただし、このような広範な構造では、2つのモデルに重要な違いがあります。

## <a name="in-this-section"></a>このセクションの内容


-   [移植できるドライバーと場所](which-drivers-can-be-ported.md)
-   [WDF ドライバーの WDM の概念](wdm-concepts-for-kmdf-drivers.md)
-   [WDM と WDF の違い](differences-between-wdm-and-kmdf.md)
-   [移植の準備](general-guidelines-for-porting.md)
-   [移植の手順](how-to-port.md)
-   [同等の KMDF と WDM の概要](summary-of-kmdf-and-wdm-equivalents.md)

 

 





