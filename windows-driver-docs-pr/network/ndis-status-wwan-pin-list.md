---
title: NDIS_STATUS_WWAN_PIN_LIST
description: ミニポート ドライバーでは、OID_WWAN_PIN_LIST の OID クエリ要求に応答する NDIS_STATUS_WWAN_PIN_LIST 通知を使用します。 ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。この通知は、NDIS_WWAN_PIN_LIST 構造体を使用します。
ms.assetid: fd8e6734-d032-445a-819a-0d5a773e9ea3
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PIN_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cd02f5297bb72fd0d69237a8fd919e2aed511f5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580098"
---
# <a name="ndisstatuswwanpinlist"></a>NDIS\_状態\_WWAN\_PIN\_一覧


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_PIN\_の OID クエリ要求に応答するリスト通知[OID\_WWAN\_PIN\_ボックスの一覧](oid-wwan-pin-list.md).

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_PIN\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff567912)構造体。

<a name="remarks"></a>コメント
-------

この目安は、OID の OID クエリ要求に応答のみ通知\_WWAN\_PIN\_一覧。 要請されていない問題は、この表示はありません。

OID の結果として発生する PIN の入力モードを変更しても\_WWAN\_暗証番号 (pin) を有効または操作を無効にする、NDIS は発生しません\_状態\_WWAN\_PIN\_一覧を示す値。

クエリ要求ごとに、ミニポート ドライバーですべてのデバイスをサポートするピンの現在の PinMode が現在の状態を反映するように更新する必要がありますに注意してください。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_PIN\_一覧](oid-wwan-pin-list.md)

[**NDIS\_WWAN\_PIN\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff567912)

 

 




