---
title: NDIS_STATUS_RING_STATUS
description: NDIS_STATUS_RING_STATUS 状態では、行のリングの状態を示します。 対応 WAN ミニポート ドライバーは、この状態を使用して、リングがエラーを報告できます。
ms.assetid: 8971eeea-13ff-47d5-8167-83c061cad054
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RING_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9ea2cd06b4ab5d036b3a572d8420945cd6d03fb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385073"
---
# <a name="ndisstatusringstatus"></a>NDIS\_状態\_リング\_状態


NDIS\_状態\_リング\_ステータスが行のリングの状態を示します。 対応 WAN ミニポート ドライバーは、この状態を使用して、リングがエラーを報告できます。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降の WAN ミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[実装いる CoNDIS WAN ミニポート ドライバー (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546752(v=vs.85))します。

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))関数には、状態値は次のいずれかで ULONG 値が含まれています。

NDIS\_リング\_ローブ\_ワイヤ\_エラー

NDIS\_リング\_ハード\_エラー

NDIS\_リング\_信号\_損失

これらの値は、状態表示の理由であるリング条件を指定します。 NDIS の詳細については\_状態\_リング\_状態を参照してください[ハードウェアの状態を報告する (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564044(v=vs.85))します。

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


[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))

 

 




