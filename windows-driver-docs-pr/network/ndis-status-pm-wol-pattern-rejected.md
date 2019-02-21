---
title: NDIS_STATUS_PM_WOL_PATTERN_REJECTED
description: NDIS_STATUS_PM_WOL_PATTERN_REJECTED 状態は、電源管理の wake on LAN (WOL) パターンが拒否されたドライバーの関連を示します。
ms.assetid: 49180c69-a3b8-4a6f-b34f-93e063c88f43
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WOL_PATTERN_REJECTED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2e1448707fc13435ea58e8e7c0fbeef8a645def9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531706"
---
# <a name="ndisstatuspmwolpatternrejected"></a>NDIS\_状態\_PM\_WOL\_パターン\_拒否済み


NDIS\_状態\_PM\_WOL\_パターン\_拒否済みの状態が電源管理の wake on LAN (WOL) パターンが拒否されたドライバーを関連することを示します。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーは、NDIS を生成できる\_状態\_PM\_WOL\_パターン\_WOL パターンを削除してのいずれかの拒否の状態を示す値。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体には WOL パターン識別子の ULONG が含まれています、WOL パターンを拒否します。 NDIS WOL パターンの識別子を提供する、 **PatternId**のメンバー、 [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)構造体。

NDIS 生成、NDIS\_状態\_PM\_WOL\_パターン\_拒否状態の表示と、そのネットワーク アダプターから以前に追加された WOL パターンを削除する必要があります。 たとえば、NDIS より高い優先順位 WOL パターンのリソースを解放する WOL パターンを削除する場合があります。 Notification イベントは、削除のパターンを追加するバインディングにのみ送信されます。

パターンをオフロードし、インフラストラクチャの間でローミングするインフラストラクチャの要素を使用するワイヤレス ネットワーク アダプターでは、新しいインフラストラクチャ要素が 1 つ前と同じ機能をサポートしていないことことができます。 ここでは、ミニポート ドライバーは、NDIS の状態の表示を発行できます NDIS を発行する NDIS および\_状態\_PM\_WOL\_パターン\_固有のエラー コードで拒否されます。

WiFi ドライバーは、ウェイク アップのパターンをローカルにキャッシュ可能性があります。 ドライバーの追加や削除、ウェイク アップ パターンの OID を処理するときのみ、ローカル キャッシュを更新するドライバーを選択できます。 受信するまで、ドライバーは、インフラストラクチャの更新を遅らせることができます、 [OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768) OID。

インフラストラクチャでは、すべてのウェイク アップのパターンに対応するために十分なリソースがあります。 ここでは、インフラストラクチャでは、ウェイク アップ パターンの一覧の一部を受け入れることができます。 ミニポート ドライバーが、OID が完了したとき\_PM\_パラメーターが要求を設定、ドライバーは、NDIS を行う必要があります\_状態\_PM\_WOL\_パターン\_拒否済みの状態各アクセス ポイント (AP) を拒否する WOL パターンの兆候です。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)

 

 




