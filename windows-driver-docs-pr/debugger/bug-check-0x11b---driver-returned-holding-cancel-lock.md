---
title: Bug Check 0x11B DRIVER_RETURNED_HOLDING_CANCEL_LOCK
description: DRIVER_RETURNED_HOLDING_CANCEL_LOCK のバグ チェックでは、0x0000011B の値を持ちます。
ms.assetid: 8728dc74-cf21-490f-b3b0-1513d2310461
keywords:
- Bug Check 0x11B DRIVER_RETURNED_HOLDING_CANCEL_LOCK
- DRIVER_RETURNED_HOLDING_CANCEL_LOCK
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_HOLDING_CANCEL_LOCK
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645ff1f64e4ca9637f93b8493170db1724351021
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238433"
---
# <a name="bug-check-0x11b-driverreturnedholdingcancellock"></a>バグ チェック 0x11B:ドライバー\_から返された\_を保持している\_キャンセル\_ロック


ドライバー\_から返された\_を保持している\_キャンセル\_ロックのバグ チェックが 0x0000011B の値を持ちます。 このバグ チェックでは、ドライバーがから返されることを示します、*キャンセル*グローバルを保持するルーチンがロックをキャンセルします。 以降のすべてのキャンセル呼び出しが失敗の原因し、いずれかの結果、デッドロックや別のバグを確認します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="driverreturnedholdingcancellock-parameters"></a>ドライバー\_から返された\_を保持している\_キャンセル\_ロック パラメーター


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
<td align="left"><p>1</p></td>
<td align="left"><p>取り消された IRP のアドレス (が有効でない)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>アドレス、<em>キャンセル</em>ルーチン。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

キャンセル スピン ロックがリリースされる必要がありますが、*キャンセル*ルーチン。

ドライバーは、個々 の I/O 要求パケット (IRP) をキャンセルする IoCancelIrpIoCancelIrp 関数を呼び出します。 この関数は、キャンセル スピン ロックを取得の IRP でキャンセル フラグを設定しを呼び出して、*キャンセル*ルーチンが指定されている場合に、IRP の適切なフィールドで指定されたルーチン。 *キャンセル*キャンセル スピン ロックを解除するルーチンが必要です。 ある場合ありません*キャンセル*、日常的なキャンセル スピン ロックが解放します。

 

 




