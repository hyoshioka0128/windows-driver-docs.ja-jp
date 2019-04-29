---
title: NDIS_STATUS_WDI_INDICATION_DISASSOCIATION
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION を使用して、ポートが、ネットワークから切断されたことを示します。
ms.assetid: 4e3ed3ed-1b96-49ea-b60f-a36d2a3fc082
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_DISASSOCIATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d0cd33ea71914854021d1f815f6cd58cd44f239
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330588"
---
# <a name="ndisstatuswdiindicationdisassociation"></a>NDIS\_状態\_WDI\_INDICATION\_関連付けの解除


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_関連付けの解除をポートが、ネットワークから切断されたことを示します。

| オブジェクト |
|--------|
| ポート   |

 

切断は、オペレーティング システムからのコマンドによってトリガーされるまたはネットワークからトリガーされる可能性があります。 トリガーされたネットワーク切断から関連付け解除または deauthentication のパケットの受信を明示的な場合がありますか、ポートに接続されているピアのプレゼンスを検出できないときに暗黙的な可能性があります。

ポートは、関連付けの解除を示す値が送信される前にこのピアに関連付けられている状態を消去する必要があります。 これには、任意のキーとこのピアに関連付けられている 802.1 x ポート承認情報が含まれます。 ポートでは、単独でのローミングがトリガーされない必要があります。

## <a name="payload-data"></a>ペイロード データ


| 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_戻せません\_INDICATION\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926292) |   |   | 関連付けの解除を示す値のパラメーターです。 |
| [**WDI\_TLV\_DISCONNECT\_DEAUTH\_FRAME**](https://msdn.microsoft.com/library/windows/hardware/dn926296) |   | x | 受信した deauthentication フレーム。 これは、802.11 MAC ヘッダーには含まれません。 |
| [**WDI\_TLV\_切断\_戻せません\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/dn926298) |   | x | 受信した関連付けの解除フレーム。 これは、802.11 MAC ヘッダーには含まれません。 | 

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


[OID\_WDI\_タスク\_切断](oid-wdi-task-disconnect.md)

[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)

 

 




