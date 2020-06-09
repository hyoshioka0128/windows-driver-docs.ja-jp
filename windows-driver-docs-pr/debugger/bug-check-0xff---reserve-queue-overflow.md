---
title: バグチェック 0xFF RESERVE_QUEUE_OVERFLOW
description: RESERVE_QUEUE_OVERFLOW バグチェックの値は0x000000FF です。 これは、予約キューに新しい項目を挿入しようとしたためにキューがオーバーフローすることを示します。
ms.assetid: d327ea41-c568-49f6-8b37-183533fd6261
keywords:
- バグチェック 0xFF RESERVE_QUEUE_OVERFLOW
- RESERVE_QUEUE_OVERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESERVE_QUEUE_OVERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 898e2e8608fe40bc455fffc32d10c6e671e05156
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534507"
---
# <a name="bug-check-0xff-reserve_queue_overflow"></a>バグチェック 0xFF: 予約 \_ キュー \_ オーバーフロー


予約 \_ キューの \_ オーバーフローバグチェックの値は、0x000000ff です。 これは、予約キューに新しい項目を挿入しようとしたためにキューがオーバーフローすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="reserve_queue_overflow-parameters"></a>予約 \_ キューの \_ オーバーフローパラメーター


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
<td align="left"><p>予約キューのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約キューのサイズ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解像度 
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに非常に役立ちます。
 

 




