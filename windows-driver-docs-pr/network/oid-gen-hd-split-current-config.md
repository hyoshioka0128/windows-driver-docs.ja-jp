---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: クエリとして重なってドライバーまたは管理ユーティリティを使用できます OID_GEN_HD_SPLIT_CURRENT_CONFIG OID ミニポート アダプターの現在のヘッダー データ分割構成を確認します。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -OID_GEN_HD_SPLIT_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bffe555573f5809d975e41816bef8e0828d7a3ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369124"
---
# <a name="oidgenhdsplitcurrentconfig"></a>OID\_GEN\_HD\_分割\_現在\_構成


クエリとしてドライバーまたは管理ユーティリティを重なってできます OID を使用\_GEN\_HD\_分割\_現在\_して現在のヘッダー データを特定の構成の OID 分割ミニポートの構成アダプター。 システム管理者は、WMI インターフェイスを通じてこの OID に関連付けられている GUID を使用できます。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーに代わってこの OID を処理します。 NDIS に現在のヘッダー データの分割、ミニポート ドライバーと初期化の属性に基づく構成情報は、および[ **NDIS\_状態\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状態を示す値。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)構造体。

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
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_現在\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_状態\_HD\_分割\_現在\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)

 

 




