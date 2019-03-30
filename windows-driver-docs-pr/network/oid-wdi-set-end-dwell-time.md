---
title: OID_WDI_SET_END_DWELL_TIME
description: OID_WDI_SET_END_DWELL_TIME を WDI にまでにフォロー アップ操作のフレームを送信する前にしばらく時間がある場合、またはプロトコル シーケンスが完了すると、通常、アクションのフレームの交換中に送信されます。
ms.assetid: 8ED1FDB1-BFDB-4522-8FF8-00D3B59EE43C
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_END_DWELL_TIME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e6a8769db6f39033d33e9d04d209ca782cc03809
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578825"
---
# <a name="oidwdisetenddwelltime"></a>OID\_WDI\_設定\_エンド\_熟考\_時間


OID\_WDI\_設定\_エンド\_熟考\_時間は WDI にまでにフォロー アップ操作のフレームを送信する前にしばらく時間がある場合、またはプロトコル シーケンスの場合、通常、アクションのフレームの交換中に送信完了します。 このコマンドは、デバイスのポートまたはステーションのポートに送信できます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | いいえ                       | 1                               |

 

このコマンドの受信後は、ファームウェアをもたらす WDI にアクションのフレームを送信するコマンドが送信されるときに指定されたチャネルを停止できます。 熟考時間が切れている場合、ファームウェアは、このコマンドを無視してください。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
必要条件
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

 

 



