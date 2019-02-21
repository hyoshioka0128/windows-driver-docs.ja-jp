---
title: 高いレベルのドライバーへのネットワーク データの受信を示す
description: 高いレベルのドライバーへのネットワーク データの受信を示す
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac4bb97a5a664978159a5cae81afd6292eb7cb7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535490"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>高いレベルのドライバーへのネットワーク データの受信を示す





コネクションレス中間ドライバーでは、呼び出すことで、[次へ] 以上のドライバーをネットワーク データを受信を示す、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数。 接続指向の中間ドライバーでは、呼び出すことで、[次へ] 以上のドライバーをネットワーク データを受信を示す、 [ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)関数。

前に、受信ネットワーク データより高度なドライバーで、データは、おそらく、形式に変換することが想定されているドライバーのプロセスを示すと、必要な場合は、中間にドライバーで割り当てられたに関連付けられているMDLsに関連するデータをコピー[**NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

 

 





