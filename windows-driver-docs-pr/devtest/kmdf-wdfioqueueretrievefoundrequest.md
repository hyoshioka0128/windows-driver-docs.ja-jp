---
title: WdfIoQueueRetrieveFoundRequest ルール (kmdf)
description: WdfIoQueueRetrieveFoundRequest ルールでは、WdfIoQueueFindRequest が呼び出され、状態が返された後のみに、WdfIoQueueRetrieveFoundRequest メソッドを呼び出すことを指定します\_同じ要求に成功した場合とない WdfObjectDereference と呼びます。
ms.assetid: CF545174-5E6D-429B-AC6D-BA7A84852FC1
ms.date: 05/21/2018
keywords:
- WdfIoQueueRetrieveFoundRequest ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfIoQueueRetrieveFoundRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 436ba78ee6f78946144fb95becd078b3d14bdf14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580782"
---
# <a name="wdfioqueueretrievefoundrequest-rule-kmdf"></a>WdfIoQueueRetrieveFoundRequest ルール (kmdf)


**WdfIoQueueRetrieveFoundRequest**ルールを指定する[ **WdfIoQueueRetrieveFoundRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548456)後のみメソッドが呼び出された[ **WdfIoQueueFindRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547415)呼び出され、状態が返されました\_成功と no [ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)が同じ要求で呼び出されます。

場合[ **WdfIoQueueFindRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547415)ステータスを返します\_出力要求の参照カウントをインクリメント成功オブジェクト、ドライバーを呼び出す必要があります[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)終了後にこの要求ハンドルを使用します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WdfIoQueueRetrieveFoundRequest</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**WdfIoQueueFindRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547415)
[**WdfIoQueueRetrieveFoundRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548456)
[**WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
 

 





