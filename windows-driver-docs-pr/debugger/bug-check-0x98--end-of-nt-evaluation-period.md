---
title: バグ チェック 0x98 END_OF_NT_EVALUATION_PERIOD
description: END_OF_NT_EVALUATION_PERIOD のバグ チェックでは、0x00000098 の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムの試用期間が終了することを示します。
ms.assetid: e49ea686-27b9-4743-9339-766b4748e29b
keywords:
- バグ チェック 0x98 END_OF_NT_EVALUATION_PERIOD
- END_OF_NT_EVALUATION_PERIOD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- END_OF_NT_EVALUATION_PERIOD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4199736c6fa853390c335239d1eaeb7f77d055a3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519109"
---
# <a name="bug-check-0x98-endofntevaluationperiod"></a>バグ チェック 0x98:終了\_の\_NT\_評価\_期間


末尾\_の\_NT\_評価\_期間のバグ チェックが 0x00000098 の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムの試用期間が終了することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="endofntevaluationperiod-parameters"></a>終了\_の\_NT\_評価\_期間パラメーター


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
<td align="left"><p>製品の有効期限の日付の下位 32 ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>製品の有効期限の日付の上位 32 ビット</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows オペレーティング システムのインストールは、有効期限の日付で評価単位です。 試用期間が。

 

 




