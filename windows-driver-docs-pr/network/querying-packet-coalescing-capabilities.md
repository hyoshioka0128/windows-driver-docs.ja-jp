---
title: パケット結合機能のクエリ
description: パケット結合機能のクエリ
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2b8c656d99a9816ab5884517a2c49a529e00e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353304"
---
# <a name="querying-packet-coalescing-capabilities"></a>パケット結合機能のクエリ


ミニポート ドライバーが初期化されると、ドライバーとアプリケーションの関連でネットワーク アダプターのパケットの結合機能を取得する次の OID クエリ要求を発行できます。

-   [OID\_受信\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

-   [OID\_受信\_フィルター\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

-   [OID\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS ドライバーが呼び出されたときに、ミニポート ドライバーが登録されているパケット結合機能を返しますの NDIS ミニポート ドライバーにこれらの OID クエリ要求を処理および[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 そのため、これらの OID クエリ要求はミニポート ドライバーでは処理されません。

結合機能を参照してください、ミニポート ドライバーがそのパケットを登録する方法の詳細については[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)します。

 

 





