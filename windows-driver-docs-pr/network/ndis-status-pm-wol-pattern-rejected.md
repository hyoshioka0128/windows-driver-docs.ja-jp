---
title: NDIS_STATUS_PM_WOL_PATTERN_REJECTED
description: NDIS_STATUS_PM_WOL_PATTERN_REJECTED の状態は、電源管理の wake on LAN (WOL) パターンが拒否されたことを示します。
ms.assetid: 49180c69-a3b8-4a6f-b34f-93e063c88f43
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WOL_PATTERN_REJECTED ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: c03d74ba9fd8c956ef0d3bfb5fc28930b36cd945
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843533"
---
# <a name="ndis_status_pm_wol_pattern_rejected"></a>NDIS\_状態\_PM\_WOL\_パターン\_拒否されました


NDIS\_ステータス\_PM\_WOL\_パターン\_拒否状態は、電源管理 wake on LAN (WOL) パターンが拒否されたことを示します。

<a name="remarks"></a>注釈
-------

NDIS またはミニポートドライバーでは、NDIS\_ステータス\_PM\_WOL\_パターンが生成されます。いずれかの\_が WOL パターンを削除すると、拒否された状態が示されます。 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーは、拒否された wol パターンの WOL パターン識別子の ULONG を含みます。 NDIS では、 [**ndis\_PM\_wol\_pattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体の**PATTERNID**メンバーに wol パターン識別子が指定されています。

NDIS は、以前に追加された WOL パターンをネットワークアダプターから削除する必要がある場合に、NDIS\_STATUS\_PM\_WOL\_パターン\_拒否状態を示します。 たとえば、NDIS は、高い優先順位の WOL パターンのリソースを解放するために WOL パターンを削除する場合があります。 Notification イベントは、削除されたパターンを追加したバインディングにのみ送信されます。

インフラストラクチャ要素を使用するワイヤレスネットワークアダプターで、インフラストラクチャを介してパターンのオフロードとローミングを行う場合は、新しいインフラストラクチャ要素が前のものと同じ機能をサポートしていない可能性があります。 この場合、ミニポートドライバーは NDIS に状態を示す状態を発行します。 NDIS は、特定のエラーコードによって拒否された\_\_PM\_WOL\_\_パターンを発行します。

WiFi ドライバーによって、ウェイクアップパターンがローカルにキャッシュされる場合があります。 ドライバーがウェイクアップパターンを追加または削除するための OID を処理する場合、ドライバーはローカルキャッシュの更新のみを選択できます。 ドライバーは、 [oid\_PM\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters) oid を受け取るまで、インフラストラクチャの更新を遅らせることができます。

インフラストラクチャには、すべてのウェイクアップパターンに対応するのに十分なリソースがない可能性があります。 この場合、インフラストラクチャはウェイクアップパターンの一部を受け入れることができます。 ミニポートドライバーが OID\_PM\_PARAMETERS set 要求を完了すると、ドライバーは、アクセスする各 WOL パターンについて、NDIS\_ステータス\_PM\_WOL\_PATTERN を作成する必要があります。ポイント (AP) は拒否します。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)

 

 




