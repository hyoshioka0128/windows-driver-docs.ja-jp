---
title: C28156
description: 警告 C28156 実際の IRQL は、必要な IRQL 一貫性がありません。
ms.assetid: dc9c108f-adf1-4364-9d2b-711c8c9db939
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28156
ms.openlocfilehash: 21851e4e6fb8a9b1af265a6309b9a6a17a3ddd7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361509"
---
# <a name="c28156"></a>C28156


C28156 を警告します。実際の IRQL は適切な IRQL と一致しません

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>終了時の値は、予期される値は設定されませんでした。</p></td>
</tr>
</tbody>
</table>

 

 **\_IRQL\_必要\_** 注釈は、関数が完了すると、ドライバーの少なくとも 1 つのパスがある場合に、ドライバーが特定の IRQL で実行することを指定します関数が完了したときに、さまざまな IRQL で実行しています。

 

 





