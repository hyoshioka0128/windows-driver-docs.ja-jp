---
title: WDM インターフェイスの制限
description: WDM インターフェイスの制限
ms.assetid: 89f3793e-8561-4d8a-a01a-1ff7aecca64a
keywords:
- KMDF WDK、WDM
- カーネルモードドライバーフレームワーク WDK、WDM
- WDM ドライバー WDK KMDF
- フレームワークベースのドライバー WDK KMDF、WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa7ed080c118df0c0fb4974384207a9c9eae944c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842794"
---
# <a name="wdm-interface-restrictions"></a>WDM インターフェイスの制限


\[は KMDF にのみ適用され\]




フレームワークベースのドライバーが WDM インターフェイスにアクセスする場合は、次の制限事項に注意する必要があります。

-   フレームワークがこのメンバーを使用するため、フレームワークベースのドライバーは、 [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)構造体の**末尾のオーバーレイ**を使用することはできません。

 

 





