---
title: NDIS_STATUS_RING_STATUS
description: NDIS_STATUS_RING_STATUS 状態では、行のリングの状態を示します。 対応 WAN ミニポート ドライバーは、この状態を使用して、リングがエラーを報告できます。
ms.assetid: 8971eeea-13ff-47d5-8167-83c061cad054
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RING_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4f3b2fecb835899e7f057453351ed3df87a71972
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560887"
---
# <a name="ndisstatusringstatus"></a>NDIS\_状態\_リング\_状態


NDIS\_状態\_リング\_ステータスが行のリングの状態を示します。 対応 WAN ミニポート ドライバーは、この状態を使用して、リングがエラーを報告できます。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降の WAN ミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[実装いる CoNDIS WAN ミニポート ドライバー (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)します。

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)関数には、状態値は次のいずれかで ULONG 値が含まれています。

NDIS\_リング\_ローブ\_ワイヤ\_エラー

NDIS\_リング\_ハード\_エラー

NDIS\_リング\_信号\_損失

これらの値は、状態表示の理由であるリング条件を指定します。 NDIS の詳細については\_状態\_リング\_状態を参照してください[ハードウェアの状態を報告する (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff564044)します。

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


[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




