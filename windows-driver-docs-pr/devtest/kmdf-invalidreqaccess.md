---
title: InvalidReqAccess ルール (kmdf)
description: InvalidReqAccess ルールでは、要求が完了したか取り消された後にアクセスしていないことを指定します。
ms.assetid: dc7609a5-8b18-44b9-88b0-a9616bc220d4
ms.date: 05/21/2018
keywords:
- InvalidReqAccess ルール (kmdf)
topic_type:
- apiref
api_name:
- InvalidReqAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdd9b2cb95ed06280dacaab00c9b0d5986497a7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536094"
---
# <a name="invalidreqaccess-rule-kmdf"></a>InvalidReqAccess ルール (kmdf)


**InvalidReqAccess**ルールでは、要求が完了したか取り消された後にアクセスしていないことを指定します。 このルールが二重の完了をチェックする規則などの他のルールでは、重複するまたは要求をチェックする規則マークされているキャンセル可能な 2 つの時刻。

要求が完了すると、キャンセル可能なマークされている場合は無効と見なされますまたは送信された後にキャンセルします。 要求を渡すことはできません、要求は無効とみなされる後、**WdfRequest * * * Xxx*関数、ドライバーを呼び出す場合を除く**WdfRequestUnmarkCancelable**要求が以前にマークされている場合キャンセル可能です。

このルールと似ています、 [ **InvalidReqAccessLocal** ](kmdf-invalidreqaccesslocal.md)ルールですただし、、 **InvalidReqAccessLocal**ルールは既定の I/O キュー コールバック内でのみ実行されます。関数。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>InvalidReqAccess</strong>ルール。</p>
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

[**WdfRequestAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff549938)
[**WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941) 
 [ **WdfRequestChangeTarget**](https://msdn.microsoft.com/library/windows/hardware/ff549943)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) 
 [**WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)
[**WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958) 
 [**WdfRequestGetCompletionParams**](https://msdn.microsoft.com/library/windows/hardware/ff549961)
[**WdfRequestGetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff549963) 
 [**WdfRequestGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549965)
[**WdfRequestGetIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549968) 
[ **WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)
[**WdfRequestGetRequestorMode** ](https://msdn.microsoft.com/library/windows/hardware/ff549971) 
 [ **WdfRequestIsFrom32BitProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549978)
[**WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983) 
 [ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984) 
 [ **WdfRequestProbeAndLockUserBufferForRead**](https://msdn.microsoft.com/library/windows/hardware/ff549987)
[**WdfRequestProbeAndLockUserBufferForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff549989) 
[ **WdfRequestRequeue**](https://msdn.microsoft.com/library/windows/hardware/ff550012)
[**WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014) 
 [ **WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)
[**WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016) 
 [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)**](https://msdn.microsoft.com/library/windows/hardware/ff550037)
 

 





