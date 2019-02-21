---
title: NDIS_STATUS_WAN_LINE_DOWN
description: NDIS_STATUS_WAN_LINE_DOWN 状態では、対応 WAN ミニポート ドライバーがリモート ノードで確立された接続を失ったことを示します。
ms.assetid: 85904e2f-ae34-4cca-a5b9-2ec4b342672a
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_LINE_DOWN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1908977ca92a5bfcf00ee20f43ba45b2a2c80803
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530442"
---
# <a name="ndisstatuswanlinedown"></a>NDIS\_状態\_WAN\_行\_ダウン


NDIS\_状態\_WAN\_行\_ダウン状態には、対応 WAN ミニポート ドライバーがリモート ノードで確立された接続を失ったことを示します。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降の WAN ミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[実装いる CoNDIS WAN ミニポート ドライバー (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)します。

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)関数にはへのポインターが含まれています、 [ **NDIS\_MAC\_行\_ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff557057)構造体。 **NdisLinkContext**の NDIS メンバー\_MAC\_行\_ダウンが有効になっているリンクを識別します。

NDIS の詳細については\_状態\_WAN\_行\_ダウンを参照してください[を示す NDIS WAN ミニポート ドライバーの状態 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867)します。

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


[**NDIS\_MAC\_行\_ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff557057)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




