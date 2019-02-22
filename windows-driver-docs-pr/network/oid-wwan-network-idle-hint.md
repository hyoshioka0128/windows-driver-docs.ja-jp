---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT は、データのインターフェイスでのアクティブまたはアイドル状態のことが必要だかどうかに関するネットワーク インターフェイスにヒントを送信します。
ms.assetid: 1FE758C1-543A-45B4-A377-336A1307689F
ms.date: 08/08/2017
keywords: -OID_WWAN_NETWORK_IDLE_HINT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e44e2c0c399ee8ea9a1f7c65792ac167324a5892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553598"
---
# <a name="oidwwannetworkidlehint"></a>OID\_WWAN\_ネットワーク\_IDLE\_ヒント


OID\_WWAN\_ネットワーク\_IDLE\_ヒントは、データのインターフェイスでのアクティブまたはアイドル状態のことが必要だかどうかに関するネットワーク インターフェイスにヒントを送信します。 ネットワーク サービスでは、ヒューリスティックを使用して、一定期間があるネットワーク トラフィックを削減することを算出する場合、またはシステムがアイドル状態になった (コネクト スタンバイ) などを入力する場合に、インターフェイスにこの要求を通常送信するかを判断します。 ネットワーク インターフェイスを使用できますこのヒューリスティックへの入力として「高速休止期間」などの手順の実装します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求と後で使用して要求を完了するには、必要な作業、 [ **NDIS\_WWAN\_ネットワーク\_IDLE\_ヒント**](https://msdn.microsoft.com/library/windows/hardware/dn931088)ネットワーク アイドル状態のヒントを示す構造体。

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
<td><p>Windows 10 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ネットワーク\_IDLE\_ヒント**](https://msdn.microsoft.com/library/windows/hardware/dn931088)

 

 




