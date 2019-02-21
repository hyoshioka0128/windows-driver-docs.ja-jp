---
title: OID_WWAN_PIN_EX
description: OID_WWAN_PIN_EX を設定または暗証番号 (Pin) に関連する拡張情報を取得します。
ms.assetid: 4D3D91B2-7B3C-4C8F-B98F-0F9999D04C03
ms.date: 08/08/2017
keywords: -OID_WWAN_PIN_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5690bd936de7c1cf7dd74205d5713c9779b015dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530540"
---
# <a name="oidwwanpinex"></a>OID\_WWAN\_PIN\_例


OID\_WWAN\_PIN\_EX が暗証番号 (Pin) に関連する拡張情報を取得または設定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)セットまたはクエリの要求が完了しているときに、状態の通知。

ミニポート ドライバーに送信する必要があります[ **NDIS\_状態\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)を格納している状態の通知、 [ **NDIS\_WWAN\_PIN\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567911) MB デバイスまたはサブスクライバーのロックを解除する PIN が必要かどうかを示すために主に、暗証番号 (pin) 型と PIN の入力の状態情報を返す構造体Identity モジュール (SIM カード) クエリ要求を完了するとき。

呼び出し元がピンに関連する情報を設定する要求を提供、 [ **NDIS\_WWAN\_設定\_PIN\_EX** ](https://msdn.microsoft.com/library/windows/hardware/hh439842)構造体には、ミニポート ドライバーをMB デバイス、有効化または無効にする PIN 設定や、SIM で PIN を変更する、暗証番号 (pin) を送信します。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




