---
title: WDI_TLV_P2P_SERVICE_TRANSACTION_ID
description: WDI_TLV_P2P_SERVICE_TRANSACTION_ID は、ANQP クエリ要求に使用するサービスのトランザクション ID を含む TLV です。
ms.assetid: 93CBE158-4595-40FC-A574-B818B2324DBF
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_TRANSACTION_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8be04495b3fa32b2447fb26f965ec6874cd0c5d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529957"
---
# <a name="wditlvp2pservicetransactionid"></a>WDI\_TLV\_P2P\_サービス\_トランザクション\_ID


WDI\_TLV\_P2P\_サービス\_トランザクション\_ID は、TLV ANQP クエリ要求に使用するサービスのトランザクション ID を格納します。

## <a name="tlv-type"></a>TLV 型


0x116

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                       |
|-------|-------------------------------------------------------------------|
| UINT8 | ANQP クエリ要求に使用するサービスのトランザクション ID。 |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




