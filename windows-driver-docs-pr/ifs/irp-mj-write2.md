---
title: IRP_MJ_WRITE 操作の Oplock の状態を確認
description: IRP_MJ_WRITE 操作の Oplock の状態を確認
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0933098d31497029f47e57097b9a646def7e60e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550122"
---
# <a name="checking-the-oplock-state-of-an-irpmjwrite-operation"></a>IRP_MJ_WRITE 操作の Oplock の状態を確認


次の場合のみ適用されます、*ストリーム*が書き込まれると、書き込みがページング I/O ではありません。

<table>
<tr>
<th>要求の種類</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>レベル 1</p>
<p>Batch (バッチ)</p>
<p>フィルター</p>
<p>読み取りハンドル</p>
<p>読み取り/書き込み</p>
<p>書き込みハンドルの読み取り</p>
</td>
<td>
<p>IRP_MJ_WRITE で壊れている場合。</p>
<ul>
<li>
<p> 書き込み操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p> [なし] に中断します。</p>
</li>
<li>
<p> ハンドルの読み取り要求。中断の受信確認は必須ですが、すぐに (受信確認を待機することがなくなど) の操作が続行します。</p>
</li>
<li>
<p> 他のすべての要求タイプ。操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read</p>
</td>
<td>
<p>IRP_MJ_WRITE で壊れている場合。</p>
<ul>
<li>
<p> 書き込み操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p> [なし] に中断します。</p>
</li>
<li>
<p> 受信確認は必要ありません、すぐに、操作を続行します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>レベル 2</p>
</td>
<td>
<ul>
<li>
<p> [なし] に常に中断します。</p>
</li>
<li>
<p> 受信確認は必要ありません、すぐに、操作を続行します。</p>
</li>
</ul>
</td>
</tr>
</table>
 

 




