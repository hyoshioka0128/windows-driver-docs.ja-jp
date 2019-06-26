---
title: WDM から WDF へのドライバーの移植
description: このセクションのトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーまたはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバーに既存の WDM ドライバーを変換する方法について説明します。
ms.assetid: 3B4D677D-2FCC-45A1-95B4-DA9CA9D7B452
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f637734d3bd5a8902166bd6e36b0cc237d18eaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372100"
---
# <a name="porting-a-driver-from-wdm-to-wdf"></a>WDM から WDF へのドライバーの移植


このセクションのトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーまたはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバーに既存の WDM ドライバーを変換する方法について説明します。

アーキテクチャ上、Windows Driver Frameworks (WDF) ドライバーは WDM ドライバーに似ています。 WDM ドライバーから成る、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数では、さまざまなディスパッチをオペレーティング システムがサービスの I/O 要求、およびその他のドライバー固有のユーティリティ関数を呼び出すルーチン。 WDF ドライバーから成る、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数、さまざまなサービスの I/O 要求にフレームワークから呼び出されるイベント コールバック関数、および追加のドライバー固有のユーティリティ関数。 ただし、この広範な構造内では、2 つのモデルと、重要な違いがあります。

## <a name="in-this-section"></a>このセクションの内容


-   [ドライバーを移植することができますが、](which-drivers-can-be-ported.md)
-   [ドライバーを WDF WDM 概念](wdm-concepts-for-kmdf-drivers.md)
-   [WDM と WDF の違い](differences-between-wdm-and-kmdf.md)
-   [移植の準備](general-guidelines-for-porting.md)
-   [移植の手順](how-to-port.md)
-   [KMDF と WDM 対応の概要](summary-of-kmdf-and-wdm-equivalents.md)

 

 





