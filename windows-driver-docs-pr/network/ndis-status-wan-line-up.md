---
title: NDIS_STATUS_WAN_LINE_UP
description: NDIS_STATUS_WAN_LINE_UP 状態では、対応 WAN ミニポート ドライバーがリモート ノードとの接続を確立されていることを示します。
ms.assetid: 1eb9d934-871a-4d95-b04f-d0b174716c98
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_LINE_UP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5596820fc36c8b6ea790b8992db8916fd2ac9459
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392389"
---
# <a name="ndisstatuswanlineup"></a>NDIS\_状態\_WAN\_行\_を


NDIS\_状態\_WAN\_行\_状態には、対応 WAN ミニポート ドライバーがリモート ノードとの接続を確立されていることを示します。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降の WAN ミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[実装いる CoNDIS WAN ミニポート ドライバー (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)します。

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)関数にはへのポインターが含まれています、 [ **NDIS\_MAC\_行\_を**](https://msdn.microsoft.com/library/windows/hardware/ff557058)構造体。

NDIS の詳細については\_状態\_WAN\_行\_を参照してください[Line-Up を示す値 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549189)と[を示す NDIS WAN ミニポート ドライバーの状態 (NDIS 5.1)。](https://msdn.microsoft.com/library/windows/hardware/ff546867).

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


[**NDIS\_MAC\_行\_を**](https://msdn.microsoft.com/library/windows/hardware/ff557058)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




