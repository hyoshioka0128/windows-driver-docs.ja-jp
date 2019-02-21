---
title: ReqDelete ルール (kmdf)
description: ReqDelete ルールでは、ドライバーが作成した要求が WdfRequestCompleteXxx 関数に渡されないというを指定します。 代わりに、要求は、完了時に削除する必要があります。
ms.assetid: 66e86353-46f7-4aa4-a4be-16277f4924e3
ms.date: 05/21/2018
keywords:
- ReqDelete ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqDelete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86c8e0b0e66490b82936c30e4a7873dc01e1392b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551915"
---
# <a name="reqdelete-rule-kmdf"></a>ReqDelete ルール (kmdf)


**ReqDelete**ルールを指定するドライバーが作成した要求は渡されないという*WdfRequestCompleteXxx*関数。 代わりに、要求は、完了時に削除する必要があります。

ドライバーがへの呼び出しで framework 要求オブジェクトを作成するかどうかは[ **WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)を使用して要求を削除する必要があります[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)要求に、ドライバーが完了するとします。

ドライバーを呼び出すことはできません[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)要求オブジェクトに使用する関数。 *WdfRequestCompleteXxx*フレームワークが指定した要求の関数は予約されています。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqDelete</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)
 

 





