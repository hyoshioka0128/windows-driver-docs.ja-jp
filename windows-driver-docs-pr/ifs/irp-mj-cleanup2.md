---
title: IRP_MJ_CLEANUP 操作の Oplock の状態を確認
description: IRP_MJ_CLEANUP 操作の Oplock の状態を確認
ms.assetid: 5e078575-cbb8-4460-9986-4c546b8c20be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2b8e6065d57a947162f4a893ff64bdef81416d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379710"
---
# <a name="checking-the-oplock-state-of-an-irpmjcleanup-operation"></a>IRP_MJ_CLEANUP 操作の Oplock の状態を確認


次の場合のみ適用されます、*ストリーム*が閉じられています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要求の種類</th>
<th align="left">条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>レベル 1</p>
<p>Batch (バッチ)</p>
<p>フィルター</p>
<p>読み取りハンドル</p>
<p>読み取り/書き込み</p>
<p>書き込みハンドルの読み取り</p></td>
<td align="left"><ul>
<li><p>[なし] に常に中断します。</p></li>
<li><p>受信確認は必要ありません、すぐに、操作を続行します。 保留中の中断要求からの受信確認の待機中の I/O 操作 (Irp) がすぐに完了したことに注意してください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>レベル 2</p>
<p>Read</p></td>
<td align="left"><ul>
<li><p>[なし] に常に中断します。 同じストリームでその他のレベル 2、または読み取り oplock 影響がないこと以外に注意してください。この FILE_OBJECT に関連付けられている、レベル 2、または読み取り oplock のみが壊れています。</p></li>
<li><p>受信確認は必要ありません、すぐに、操作を続行します。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 




