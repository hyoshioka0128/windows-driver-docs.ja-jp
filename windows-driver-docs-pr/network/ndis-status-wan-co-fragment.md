---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状態では、いる CoNDIS WAN ミニポート ドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_FRAGMENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d625f22f6cd7e617606140be6778dedb0596088e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531715"
---
# <a name="ndisstatuswancofragment"></a>NDIS\_状態\_WAN\_CO\_フラグメント


NDIS\_状態\_WAN\_CO\_-FRAGMENT status はいる CoNDIS WAN ミニポート ドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体にはへのポインターが含まれています、 [ **NDIS\_WAN\_CO\_フラグメント**](https://msdn.microsoft.com/library/windows/hardware/ff559030)構造体。 NDIS\_WAN\_CO\_フラグメントの構造が理由を部分的なパケットが受信されたことを説明します。

NDIS の詳細については\_状態\_WAN\_CO\_フラグメントを参照してください[を示している CoNDIS WAN ミニポート ドライバー ステータス](https://msdn.microsoft.com/library/windows/hardware/ff554825)します。 いる CoNDIS WAN インターフェイスの詳細については、[いる CoNDIS の WAN ミニポート ドライバーを実装する](https://msdn.microsoft.com/library/windows/hardware/ff553805)を参照してください。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_WAN\_CO\_フラグメント**](https://msdn.microsoft.com/library/windows/hardware/ff559030)

 

 




