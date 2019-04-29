---
title: IRP_MJ_LOCK_CONTROL 操作の Oplock の状態を確認
description: IRP_MJ_LOCK_CONTROL 操作の Oplock の状態を確認
ms.assetid: 6e0a5287-9a22-465f-b345-c9af556e6cdb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf870352b31e9e894d07f60cd8c3ba9aec8562cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324240"
---
# <a name="checking-the-oplock-state-of-an-irpmjlockcontrol-operation"></a>IRP_MJ_LOCK_CONTROL 操作の Oplock の状態を確認


次はバイト範囲ロック操作のたびに、指定したストリームに適用されます。
<table>
<tr>
<th>要求の種類</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>レベル 1</p>
<p>Batch (バッチ)</p>
<p>読み取りハンドル</p>
<p>読み取り/書き込み</p>
<p>書き込みハンドルの読み取り</p>
</td>
<td>
<p>IRP_MJ_LOCK_CONTROL で壊れている場合。</p>
<ul>
<li>
<p> ロック操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
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
<p>ハンドルの要求。中断の受信確認は必須ですが、すぐに (受信確認を待機することがなくなど) の操作が続行します。</p>
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
<p>IIRP_MJ_LOCK_CONTROL で壊れている場合。</p>
<ul>
<li>
<p> ロック操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
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
<p>フィルター</p>
</td>
<td>
<ul>
<li>
<p> Oplock は破損していない、受信確認は不要ですが、および、操作をすぐに続行します。</p>
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

 

 




