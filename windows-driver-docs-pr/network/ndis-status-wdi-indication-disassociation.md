---
title: NDIS_STATUS_WDI_INDICATION_DISASSOCIATION
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION を使用して、ポートが、ネットワークから切断されたことを示します。
ms.assetid: 4e3ed3ed-1b96-49ea-b60f-a36d2a3fc082
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_DISASSOCIATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d6233fba5fdd7928aacda21b6ba0fd19e082fca4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582111"
---
# <a name="ndisstatuswdiindicationdisassociation"></a>NDIS\_状態\_WDI\_INDICATION\_関連付けの解除


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_関連付けの解除をポートが、ネットワークから切断されたことを示します。

| オブジェクト |
|--------|
| ポート   |

 

切断は、オペレーティング システムからのコマンドによってトリガーされるまたはネットワークからトリガーされる可能性があります。 トリガーされたネットワーク切断から関連付け解除または deauthentication のパケットの受信を明示的な場合がありますか、ポートに接続されているピアのプレゼンスを検出できないときに暗黙的な可能性があります。

ポートは、関連付けの解除を示す値が送信される前にこのピアに関連付けられている状態を消去する必要があります。 これには、任意のキーとこのピアに関連付けられている 802.1 x ポート承認情報が含まれます。 ポートでは、単独でのローミングがトリガーされない必要があります。

## <a name="payload-data"></a>ペイロード データ


型の複数の TLV インスタンスには、説明 (オプション) が許可されている[ **WDI\_TLV\_戻せません\_INDICATION\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/dn926292)関連付けの解除を示す値のパラメーターです。
[**WDI\_TLV\_切断\_DEAUTH\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/dn926296) X の受け取った deauthentication フレーム。 これは、802.11 MAC ヘッダーには含まれません。
[**WDI\_TLV\_切断\_戻せません\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/dn926298) X の受け取った戻せませんフレーム。 これは、802.11 MAC ヘッダーには含まれません。
 

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


[OID\_WDI\_タスク\_切断](oid-wdi-task-disconnect.md)

[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)

 

 




