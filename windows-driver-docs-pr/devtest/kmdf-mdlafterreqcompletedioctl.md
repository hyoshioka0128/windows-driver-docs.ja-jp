---
title: MdlAfterReqCompletedIoctl rule (kmdf)
description: MdlAfterReqCompletedIoctl ルールでは、EvtIoDeviceControl コールバック関数内でメモリの記述子のリスト (MDL) にアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: ce82cca4-f0e3-4e84-8599-4094fa1ed4c2
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIoctl rule (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17d4a708d3c99d12be0d7dd79415235cd60d0f2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539268"
---
# <a name="mdlafterreqcompletedioctl-rule-kmdf"></a>MdlAfterReqCompletedIoctl rule (kmdf)


**MdlAfterReqCompletedIoctl**ルールでは、ことを指定します、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数では、メモリの記述子のリスト (MDL) は、後にアクセスできませんI/O 要求が完了するとします。

ドライバーの内[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数を呼び出すことによって取得された MDL、 [ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)または[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)で、I/O 要求。

このルールは、次の MDL アクセス関数で検索します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MdlAfterReqCompletedIoctl</strong>ルール。</p>
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

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016) 
 [ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)








