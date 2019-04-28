---
title: NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION を使用して、ホストに接続するための優れたピアを検索しようとする必要がありますを示します。
ms.assetid: 25f920e9-af87-48ad-be64-aa3ebfe2db5f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a70f2320aa2bb62f0db75d3b35eca9060925fc4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361031"
---
# <a name="ndisstatuswdiindicationroamingneeded"></a>NDIS\_状態\_WDI\_INDICATION\_ローミング\_が必要


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_関連付けの解除を示す、ホストに接続するための優れたピアを検索しようとする必要があります。 この通知は、現在接続されているピアとリンクの品質が特定のしきい値を下回ったときに使用されます。 この通知を送信するには、ローミング スキャンまたは移動操作をホストが起動されます。 Microsoft コンポーネントは、移動操作を開始する前に、接続が切断を実行しません。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                    | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                         |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ローミング\_必要\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898049) |                                |          | ローミングのトリガーの理由です。 ときに、 [OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)がトリガーされると、この理由はそれに転送されます。 |

 

<a name="requirements"></a>必要条件
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


[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)

 

 




