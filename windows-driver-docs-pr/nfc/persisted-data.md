---
title: 永続化されたデータ
description: データの永続化はです。
ms.assetid: 61C3C55C-00DC-4A8C-B235-7C0391FB5119
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9475f20a802adec7143a609ce510e86ae7cec4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834055"
---
# <a name="persisted-data"></a>永続化されたデータ


レジストリの場所に関するデータの永続化については、次の説明を参照してください。

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
<th align="left">位置情報</th>
<th align="left">コンテンツ、使用法、既定値</th>
<th align="left">アクセス (既定ではない場合)</th>
<th align="left">PII は保存されていますか?</th>
<th align="left">この設定は移行されていますか?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">デバイスノードのレジストリの場所</td>
<td align="left">NfcRadioTurnedOff、DWORD:
<p>TRUE: NFC RM がオフになっています</p>
<p>FALSE: NFC RM はオンになっており、アイドル状態の電源管理が適用されます</p></td>
<td align="left">デバイスの列挙ツリーから継承します。特別な ACL セットはありません。</td>
<td align="left">該当なし</td>
<td align="left">必須ではない</td>
</tr>
</tbody>
</table>

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

