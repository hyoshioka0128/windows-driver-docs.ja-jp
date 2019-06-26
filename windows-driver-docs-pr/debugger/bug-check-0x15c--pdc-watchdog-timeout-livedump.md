---
title: バグ チェック 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
description: PDC_WATCHDOG_TIMEOUT_LIVEDUMP バグは、入力またはコネクト スタンバイの終了を防ぐ、システム コンポーネントが、応答に失敗したことを示す 0x0000015C の値を持つを確認します。
ms.assetid: 4FBB884D-99B5-4564-95D5-396323651C5A
keywords:
- バグ チェック 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a8abaaeb0e6d82416d453a04f840cab7a8918967
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362164"
---
# <a name="bug-check-0x15c-pdcwatchdogtimeoutlivedump"></a>バグ チェック 0x15C:PDC\_ウォッチドッグ\_タイムアウト\_LIVEDUMP


PDC\_ウォッチドッグ\_タイムアウト\_LIVEDUMP バグ チェックが 0x0000015C の値を持ちます。 これは、システム コンポーネントが原因でシステムが開始または終了コネクト スタンバイから割り当てられた期間内に応答する失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="pdcwatchdogtimeoutlivedump-parameters"></a>PDC\_ウォッチドッグ\_タイムアウト\_LIVEDUMP パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">ハングしたコンポーネントのクライアント ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>ハングしたコンポーネントのクライアントの種類。</p>
0x1:通知クライアントが応答に失敗しました。
<p>3 - 通知クライアントへのポインター (pdc! _PDC_NOTIFICATION_CLIENT)。</p>
<p>4 - pdc へのポインター。PDC_14F_TRIAGE 構造体。</p>
0x2:回復性クライアントは、応答に失敗しました。
<p>3-回復性のクライアントへのポインター (pdc! _PDC_RESILIENCY_CLIENT)。</p>
<p>4 - pdc へのポインター。PDC_14F_TRIAGE 構造体。</p>
0x3:アクティベーターをクライアントには、長時間の参照が保持されています。
<p>3-アクティブ化クライアントへのポインター (pdc! _PDC_ACTIVATOR_CLIENT)。</p>
<p>4 - pdc へのポインター。PDC_14F_TRIAGE 構造体。</p></td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
</tbody>
</table>

 

 

 




