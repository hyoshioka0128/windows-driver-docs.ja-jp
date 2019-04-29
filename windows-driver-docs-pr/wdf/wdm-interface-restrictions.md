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
ms.openlocfilehash: 39bbe87a759ce088a9c95b690f5ee64fce3b804d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385713"
---
# <a name="wdm-interface-restrictions"></a>WDM インターフェイスの制限


\[KMDF にのみ適用されます。\]




フレームワークに基づくドライバーが WDM インターフェイスにアクセスする場合、次の制限があります。

-   フレームワーク ベースのドライバーが使用する必要があります、 **Tail.Overlay.DriverContext**のメンバー、 [ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)フレームワークはこのメンバーを使用するために、構造体します。

 

 





