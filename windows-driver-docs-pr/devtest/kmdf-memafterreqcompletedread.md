---
title: MemAfterReqCompletedRead ルール (kmdf)
description: MemAfterReqCompletedRead ルールでは、EvtIoRead コールバック関数内で framework メモリ オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 0c19b9e3-5968-4d93-9449-96e8a93fffde
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedRead ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedRead
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ebc4598cd95a61c86991c728d2f7778f2d7d890
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579167"
---
# <a name="memafterreqcompletedread-rule-kmdf"></a>MemAfterReqCompletedRead ルール (kmdf)


**MemAfterReqCompletedRead**ルールでは、ことを指定します、 [ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)コールバック関数では、framework のメモリ オブジェクトは、I/O 要求の後にアクセスできません完了しました。

ドライバーの内[ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)コールバック関数を呼び出すことによって取得された framework メモリ オブジェクト、 [ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

このルールは、次の 2 つのメモリ アクセス方法を考慮します。

[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)
[**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MemAfterReqCompletedRead</strong>ルール。</p>
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

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015) 
 [ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)








