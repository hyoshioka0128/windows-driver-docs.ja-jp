---
title: InvalidReqAccessLocal ルール (kmdf)
description: InvalidReqAccessLocal ルールが完了したか取り消された後にアクセスされていない要求をローカルに作成を指定します。
ms.assetid: d6bf222d-93b6-4dcd-8663-ca85a8a2d203
ms.date: 05/21/2018
keywords:
- InvalidReqAccessLocal ルール (kmdf)
topic_type:
- apiref
api_name:
- InvalidReqAccessLocal
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 194ed9a42fa3d223783addfc81c76c92afa31f74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350420"
---
# <a name="invalidreqaccesslocal-rule-kmdf"></a>InvalidReqAccessLocal ルール (kmdf)


**InvalidReqAccessLocal**ルールが完了したか取り消された後にローカルで作成された要求はアクセスされませんを指定します。 このルールが二重の完了をチェックする規則などの他のルールでは、重複するまたは要求をチェックする規則マークされているキャンセル可能な 2 つの時刻。

要求が完了すると、キャンセル可能なマークされている場合は無効と見なされますまたは送信された後にキャンセルします。 要求を渡すことはできません、要求は無効とみなされる後、**WdfRequest * * * Xxx*関数、ドライバーを呼び出す場合を除く**WdfRequestUnmarkCancelable**要求が以前にマークされている場合キャンセル可能です。

このルールと似ています、 [ **InvalidReqAccess** ](kmdf-invalidreqaccess.md)ルールです。 ただし、、 **InvalidReqAccessLocal**ルールは、既定の I/O キューのコールバック関数内でのみ実行されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>InvalidReqAccessLocal</strong>ルール。</p>
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

[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)  
[**WdfRequestAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff549938)  
[**WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)  
[**WdfRequestChangeTarget**](https://msdn.microsoft.com/library/windows/hardware/ff549943)  
[**WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)  
[**WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)  
[**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)  
[**WdfRequestGetCompletionParams**](https://msdn.microsoft.com/library/windows/hardware/ff549961)  
[**WdfRequestGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff549963)  
[**WdfRequestGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549965)  
[**WdfRequestGetIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549968)  
[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)  
[**WdfRequestGetRequestorMode**](https://msdn.microsoft.com/library/windows/hardware/ff549971)  
[**WdfRequestIsFrom32BitProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549978)  
[**WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983)  
[**WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)  
[**WdfRequestProbeAndLockUserBufferForRead**](https://msdn.microsoft.com/library/windows/hardware/ff549987)  
[**WdfRequestProbeAndLockUserBufferForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff549989)  
[**WdfRequestRequeue**](https://msdn.microsoft.com/library/windows/hardware/ff550012)  
[**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)  
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)  
[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)  
[**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)  
[**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)  
[**WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)  
[**WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)  
[**WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)  
[**WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)  
[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)  
[**WdfRequestSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff550030)  
[**WdfRequestSetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550032)  
[**WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)  
[**WdfRequestWdmFormatUsingStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550036)  
[**WdfRequestWdmGetIrp**](https://msdn.microsoft.com/library/windows/hardware/ff550037)  
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)  
 

 





