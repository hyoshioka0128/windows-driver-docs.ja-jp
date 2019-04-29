---
title: IRP_MJ_READ 操作の Oplock の状態を確認
description: IRP_MJ_READ 操作の Oplock の状態を確認
ms.assetid: 9b4d1ba9-0838-44f1-8328-f60bfb3910ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4faf6bd530b129604bdf79e84b9e59f6d1e8d9bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324322"
---
# <a name="checking-the-oplock-state-of-an-irpmjread-operation"></a>IRP_MJ_READ 操作の Oplock の状態を確認


次の場合のみ適用されます、*ストリーム*は読み取られています。 TxF トランザクション リーダーの読み取りを実行する、トランザクション リーダー、ライター (つまり、oplock ことはできませんのすべてを保持しているライター) を除外するため、このチェックが行われていません。
<table>
<tr>
<th>要求の種類</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>レベル 1</p>
<p>Batch (バッチ)</p>
</td>
<td>
<p>IRP_MJ_READ で壊れている場合。</p>
<ul>
<li>
<p> 読み取り操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p> レベル 2 にブレークします。</p>
</li>
<li>
<p> 操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>読み取り/書き込み</p>
</td>
<td>
<p>IRP_MJ_READ で壊れている場合。</p>
<ul>
<li>
<p> 読み取り操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p> 読み取り専用に中断します。</p>
</li>
<li>
<p> 操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>書き込みハンドルの読み取り</p>
</td>
<td>
<p>IRP_MJ_READ で壊れている場合。</p>
<ul>
<li>
<p> 読み取り操作では、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p> 読み取りハンドルを中断します。</p>
</li>
<li>
<p> 操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>レベル 2</p>
<p>フィルター</p>
<p>Read</p>
<p>読み取りハンドル</p>
</td>
<td>
<ul>
<li>
<p> Oplock は破損していない、受信確認は不要ですが、および、操作をすぐに続行します。</p>
</li>
</ul>
</td>
</tr>
</table>

 




