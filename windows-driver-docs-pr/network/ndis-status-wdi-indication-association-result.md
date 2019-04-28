---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT を使用して、関連結果を示します。
ms.assetid: dc025aec-30f4-4a78-b449-acc49d13b507
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fb71ef33a3008a20e973dafcd59204b302088d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366408"
---
# <a name="ndisstatuswdiindicationassociationresult"></a>NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_結果


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_の関連付けの結果を示す結果。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                    |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------|
| [**WDI\_TLV\_アソシエーション\_結果**](https://msdn.microsoft.com/library/windows/hardware/dn926140) | x                              |          | 関連付けの結果の一覧。 |

 

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

 

 




