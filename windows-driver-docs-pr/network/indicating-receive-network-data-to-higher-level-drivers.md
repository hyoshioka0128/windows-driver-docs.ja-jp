---
title: 高レベル ドライバーへの受信ネットワーク データの表示
description: 高レベル ドライバーへの受信ネットワーク データの表示
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中間ドライバー WDK ネットワーク、受信操作
- NDIS 中間ドライバー WDK、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82df5e75b5b8880d7798b337e3b4418c5df96fa8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824664"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>高レベル ドライバーへの受信ネットワーク データの表示





コネクションレスな中間ドライバーは、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出して、次の上位のドライバーにネットワークデータを受信することを示します。 接続指向の中間ドライバーは、 [**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数を呼び出して、次の上位のドライバーにネットワークデータを受信することを示します。

ネットワークデータの受信を示す前に、ドライバーはデータを処理します。たとえば、上位レベルのドライバーによって想定される形式に変換します。必要に応じて、中間ドライバーによって割り当てられたネットワークに関連付けられている MDLs に関連データをコピーします。 [ **\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体。

 

 





