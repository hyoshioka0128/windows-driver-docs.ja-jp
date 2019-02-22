---
title: クエリ パケット結合機能
description: クエリ パケット結合機能
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5bf109b70aa92325922e99847fc969e86c3161f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550114"
---
# <a name="querying-packet-coalescing-capabilities"></a>クエリ パケット結合機能


ミニポート ドライバーが初期化されると、ドライバーとアプリケーションの関連でネットワーク アダプターのパケットの結合機能を取得する次の OID クエリ要求を発行できます。

-   [OID\_受信\_フィルター\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569791)

-   [OID\_受信\_フィルター\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569786)

-   [OID\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569790)

NDIS ドライバーが呼び出されたときに、ミニポート ドライバーが登録されているパケット結合機能を返しますの NDIS ミニポート ドライバーにこれらの OID クエリ要求を処理および[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 そのため、これらの OID クエリ要求はミニポート ドライバーでは処理されません。

結合機能を参照してください、ミニポート ドライバーがそのパケットを登録する方法の詳細については[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)します。

 

 





