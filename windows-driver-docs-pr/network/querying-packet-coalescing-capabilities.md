---
title: パケット結合機能のクエリ
description: パケット結合機能のクエリ
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23964e3c7f2609f41511fb53ae5af74fe4132b79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844883"
---
# <a name="querying-packet-coalescing-capabilities"></a>パケット結合機能のクエリ


ミニポートドライバーが初期化されると、その後のドライバーとアプリケーションは次の OID クエリ要求を発行して、ネットワークアダプターのパケット合体機能を取得することができます。

-   [OID\_ハードウェア\_機能\_\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

-   [OID\_現在の\_機能\_受信\_フィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

-   [グローバル\_パラメーター\_\_フィルターを受け取る OID\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS は、ミニポートドライバーに対するこれらの OID クエリ要求を処理し、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出したときにミニポートドライバーが登録したパケット合体機能を返します。 そのため、これらの OID クエリ要求は、ミニポートドライバーによって処理されません。

ミニポートドライバーによるパケット合体機能の登録方法の詳細については、「[受信フィルター機能の決定](determining-receive-filtering-capabilities.md)」を参照してください。

 

 





