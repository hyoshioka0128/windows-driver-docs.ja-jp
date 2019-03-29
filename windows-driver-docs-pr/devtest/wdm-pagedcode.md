---
title: PagedCode ルール (wdm)
description: PagedCode ルールでは、ドライバーが、ページを呼び出すことを指定します\_IRQL APC で実行されている場合にのみ、コードのマクロ\_レベル。
ms.assetid: de272bc2-8391-41b1-9526-3e135a586258
ms.date: 05/21/2018
keywords:
- PagedCode ルール (wdm)
topic_type:
- apiref
api_name:
- PagedCode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b3f650a06d5e78abcf91e55e66304b80f5455c5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581312"
---
# <a name="pagedcode-rule-wdm"></a>PagedCode ルール (wdm)


**PagedCode**ルールでは、ドライバーを呼び出すことを指定します、 [**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)マクロで実行されている場合にのみ**IRQL &lt;= APC\_レベル**します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PagedCode</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**ページングされた\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)
 

 





