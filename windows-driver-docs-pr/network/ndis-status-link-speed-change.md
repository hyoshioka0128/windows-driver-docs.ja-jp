---
title: NDIS_STATUS_LINK_SPEED_CHANGE
description: NDIS_STATUS_LINK_SPEED_CHANGE 状態では、リンク速度の変更を示します。
ms.assetid: 084e43c9-598c-4c30-8004-2d1876a1cddd
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_LINK_SPEED_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 50025c65d233ce489acf3d2fd5c4b867ff15d9e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368576"
---
# <a name="ndisstatuslinkspeedchange"></a>NDIS\_状態\_リンク\_速度\_変更


NDIS\_状態\_リンク\_速度\_状態の変更がリンク速度の変更を示します。

<a name="remarks"></a>注釈
-------

NDIS 変換 NDIS\_状態\_リンク\_速度\_変更の状態インジケーターを[ **NDIS\_状態\_リンク\_の状態**](ndis-status-link-state.md) NDIS 6.0 のドライバーを後続の状態のインジケーター。 NDIS が、NDIS を受信すると\_状態\_リンク\_速度\_状態の変更の OID クエリ要求を発行する NDIS [OID\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed). NDIS OID の結果を使用する\_GEN\_リンク\_速度クエリを発行する NDIS\_状態\_リンク\_NDIS 6.0 のドライバーに関連する状態。

NDIS 5。*x*または以前のミニポート ドライバーにある DWORD 型の値を指定する、 *StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))関数。 NDIS の詳細については\_状態\_リンク\_速度\_変更を参照してください[OID\_IRDA\_レート\_スニフ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560287(v=vs.85))します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降はサポートされていません (を使用して、 <a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"> <strong>NDIS_STATUS_LINK_STATE</strong> </a>代わりに)。 Windows Vista および Windows XP で 5.1 の NDIS ドライバーのみサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_リンク\_状態**](ndis-status-link-state.md)

[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))

[OID\_GEN\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)

[OID\_IRDA\_レート\_盗聴](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560287(v=vs.85))

 

 




