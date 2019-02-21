---
title: 永続化されたデータ
description: データ永続化されます。
ms.assetid: 61C3C55C-00DC-4A8C-B235-7C0391FB5119
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01ed73a76b4f3caa0001a791f48d54049df05c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553419"
---
# <a name="persisted-data"></a>永続化されたデータ


レジストリの場所のデータの永続化は次のように説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Location</th>
<th align="left">内容、使用状況、既定値</th>
<th align="left">アクセス (ない場合は既定値)</th>
<th align="left">PII が格納されているか。</th>
<th align="left">この設定を移行しますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">デバイス ノードのレジストリの場所</td>
<td align="left">NfcRadioTurnedOff、DWORD:
<p>TRUE:NFC RM はオフです。</p>
<p>FALSE:NFC RM アイドル状態の電源管理対象となるは、します。</p></td>
<td align="left">デバイスの列挙型ツリー、特別な ACL が設定されていませんから継承します。</td>
<td align="left">なし</td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

