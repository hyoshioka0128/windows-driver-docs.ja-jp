---
title: WDM インターフェイスの制限
description: WDM インターフェイスの制限
ms.assetid: 89f3793e-8561-4d8a-a01a-1ff7aecca64a
keywords:
- KMDF WDK、WDM
- カーネル モード ドライバー フレームワーク、WDK WDM
- WDM ドライバー WDK KMDF
- フレームワークに基づいたドライバー WDK KMDF、WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9261cc1a0d48b4b79a0782bb623fe6cff2f50fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372082"
---
# <a name="wdm-interface-restrictions"></a>WDM インターフェイスの制限


\[KMDF にのみ適用されます。\]




フレームワークに基づくドライバーが WDM インターフェイスにアクセスする場合、次の制限があります。

-   フレームワーク ベースのドライバーが使用する必要があります、 **Tail.Overlay.DriverContext**のメンバー、 [ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)フレームワークはこのメンバーを使用するために、構造体します。

 

 





