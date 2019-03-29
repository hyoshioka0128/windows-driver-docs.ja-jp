---
title: WDI_TLV_P2P_SERVICE_SESSION_INFO
description: WDI_TLV_P2P_SERVICE_SESSION_INFO では、サービスのセッション情報を含む TLV です。
ms.assetid: ED1FF2F5-82BA-48AC-A986-8B75F099DCA0
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_SESSION_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4d6daf4f042907c9b8803cd8d57e5054ba2067a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573946"
---
# <a name="wditlvp2pservicesessioninfo"></a>WDI\_TLV\_P2P\_サービス\_セッション\_情報


WDI\_TLV\_P2P\_サービス\_セッション\_情報は、サービスのセッション情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xf0 です.

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                  |
|-----------|------------------------------|
| UINT8\[\] | サービスのセッションの情報。 |

 

<a name="requirements"></a>必要条件
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

 

 




