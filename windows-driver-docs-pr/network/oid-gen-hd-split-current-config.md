---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: クエリとして重なってドライバーまたは管理ユーティリティを使用できます OID_GEN_HD_SPLIT_CURRENT_CONFIG OID ミニポート アダプターの現在のヘッダー データ分割構成を確認します。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -OID_GEN_HD_SPLIT_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7661e83c5b901833562007b6777d79a67330e1db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381332"
---
# <a name="oidgenhdsplitcurrentconfig"></a>OID\_GEN\_HD\_分割\_現在\_構成


クエリとしてドライバーまたは管理ユーティリティを重なってできます OID を使用\_GEN\_HD\_分割\_現在\_して現在のヘッダー データを特定の構成の OID 分割ミニポートの構成アダプター。 システム管理者は、WMI インターフェイスを通じてこの OID に関連付けられている GUID を使用できます。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーに代わってこの OID を処理します。 NDIS に現在のヘッダー データの分割、ミニポート ドライバーと初期化の属性に基づく構成情報は、および[ **NDIS\_状態\_HD\_分割\_現在\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567370)状態を示す値。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff565696)構造体。

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
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_現在\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff565696)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_状態\_HD\_分割\_現在\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff567370)

 

 




