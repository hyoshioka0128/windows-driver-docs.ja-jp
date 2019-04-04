---
title: MdlAfterReqCompletedRead ルール (kmdf)
description: MdlAfterReqCompletedRead ルールでは、EvtIoRead コールバック関数内で取得されたメモリ記述子のリスト (MDL) オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: d09150fd-77e8-4910-a2cb-4e7043e4b107
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedRead ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedRead
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1eb0b300d632a18e3a64f4b61de3491bcf54709a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570526"
---
# <a name="mdlafterreqcompletedread-rule-kmdf"></a>MdlAfterReqCompletedRead ルール (kmdf)


**MdlAfterReqCompletedRead**ルールでは、ことを指定します、 [ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)コールバック関数では、メモリの記述子を取得する一覧 (MDL) オブジェクトにアクセスできませんI/O 要求が完了するとします。

ドライバーの内*EvtIoRead*コールバック関数を呼び出すことによって取得された要求のバッファー、 [ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)メソッドにすることはできません呼び出した後アクセス[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

このルールでは、次の 2 つのメソッドと見なされます。

[**WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)
[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MdlAfterReqCompletedRead</strong>ルール。</p>
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

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016) 
 [ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)








