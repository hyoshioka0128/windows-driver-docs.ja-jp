---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT を使用して、関連結果を示します。
ms.assetid: dc025aec-30f4-4a78-b449-acc49d13b507
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 153d3a14bdd968de7e3349abef529236597ebf93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366641"
---
# <a name="ndisstatuswdiindicationassociationresult"></a>NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_結果


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_の関連付けの結果を示す結果。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                    |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------|
| [**WDI\_TLV\_アソシエーション\_結果**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-association-result) | x                              |          | 関連付けの結果の一覧。 |

 

<a name="requirements"></a>要件
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_タスク\_接続](oid-wdi-task-connect.md)

[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)

 

 




