---
title: MdlAfterReqCompletedReadA ルール (kmdf)
description: MdlAfterReqCompletedReadA ルールでは、EvtIoRead コールバック関数内で取得されたメモリ記述子のリスト (MDL) オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 3e7c40a0-882e-45eb-8cf1-bee1096379ad
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedReadA ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedReadA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 293624ab43a47f8bc0a936bfe67cf637d850970d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572278"
---
# <a name="mdlafterreqcompletedreada-rule-kmdf"></a>MdlAfterReqCompletedReadA ルール (kmdf)


**MdlAfterReqCompletedReadA**ルールでは、ことを指定します、 [ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)メモリ記述子のリスト (MDL) オブジェクトを取得することはできませんのコールバック関数I/O 要求が完了した後にアクセスします。

ドライバーの内*EvtIoRead*コールバック関数を呼び出すことによって取得された要求のバッファー、 [ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)メソッドにすることはできません呼び出した後アクセス[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

このルールでは、次の関数と見なされます。

[**WDF\_メモリ\_記述子\_INIT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff552396)
[**MmGetMdlByteCount** ](https://msdn.microsoft.com/library/windows/hardware/ff554530) 
[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)
[**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) 
 [**IoBuildPartialMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548324) (最初と 2 番目のパラメーター) [ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) 
 [ **MmGetMdlPfnArray**](https://msdn.microsoft.com/library/windows/hardware/ff554537)
[**MmGetMdlByteOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554533) 
 [ **MmPrepareMdlForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554660)
[**WdfDmaTransactionInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff547099)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MdlAfterReqCompletedReadA</strong>ルール。</p>
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

[**WDF\_メモリ\_記述子\_INIT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff552396)
[**WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)
 [ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)
[**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) 
 [**MmGetMdlByteCount**](https://msdn.microsoft.com/library/windows/hardware/ff554530)
[**MmGetMdlByteOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554533) 
 [ **MmGetMdlPfnArray**](https://msdn.microsoft.com/library/windows/hardware/ff554537)
[**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) 
 [ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)
[**MmPrepareMdlForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554660)








