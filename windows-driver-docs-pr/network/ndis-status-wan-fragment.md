---
title: NDIS_STATUS_WAN_FRAGMENT
description: NDIS_STATUS_WAN_FRAGMENT 状態では、対応 WAN ミニポート ドライバーがリモート ノードから部分的なパケットを受信したことを示します。
ms.assetid: 1ac00110-8b97-4905-b409-454e3d9a09e0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_FRAGMENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 97cb2a741efb0c3b950a1afefe16148dcef3e06a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560231"
---
# <a name="ndisstatuswanfragment"></a>NDIS\_状態\_WAN\_フラグメント


NDIS\_状態\_WAN\_フラグメントの状態は、対応 WAN ミニポート ドライバーがリモート ノードから部分的なパケットを受信したことを示します。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降のミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 NDIS の詳細については\_状態\_WAN\_フラグメントを参照してください[ **NDIS\_状態\_WAN\_CO\_フラグメント**](ndis-status-wan-co-fragment.md).

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)関数にはへのポインターが含まれています、 [ **NDIS\_MAC\_フラグメント**](https://msdn.microsoft.com/library/windows/hardware/ff557055)構造体。 NDIS\_MAC\_フラグメントは、特定のリンクを識別し、部分的なパケットが受信されたことの理由を説明します。

NDIS の詳細については\_状態\_WAN\_フラグメントを参照してください[を示す NDIS WAN ミニポート ドライバーの状態 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 のドライバーまたは Windows Vista または Windows XP で 5.1 の NDIS ドライバーのサポートされていません。 NDIS 4.x ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_MAC\_フラグメント**](https://msdn.microsoft.com/library/windows/hardware/ff557055)

[**NDIS\_状態\_WAN\_CO\_フラグメント**](ndis-status-wan-co-fragment.md)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




