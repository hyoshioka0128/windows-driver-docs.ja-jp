---
title: MdlAfterReqCompletedIoctlA ルール (kmdf)
description: MdlAfterReqCompletedIoctlA ルールでは、EvtIoDeviceControl コールバック関数内でメモリの記述子のリスト (MDL) にアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 694d3370-d739-4d6b-abc1-636eb90ea0b3
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b626bd9b736c79ef0f2b4f065064a0543f94fcb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536822"
---
# <a name="mdlafterreqcompletedioctla-rule-kmdf"></a>MdlAfterReqCompletedIoctlA ルール (kmdf)


**MdlAfterReqCompletedIoctlA**ルールでは、ことを指定します、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数では、メモリの記述子のリスト (MDL) にアクセスできませんI/O 要求が完了するとします。

ドライバーの内[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数を呼び出すことによって取得された MDL、 [ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)または[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)で、I/O 要求。

このルールは次の 2 つの MDL へのアクセス方法を確認します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MdlAfterReqCompletedIoctlA</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**WDF\_メモリ\_記述子\_INIT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff552396)
[**WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)
 [ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)
[**IoBuildPartialMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548324) 
[ **KeFlushIoBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff552041)
[**MmGetMdlByteCount** ](https://msdn.microsoft.com/library/windows/hardware/ff554530) 
 [ **MmGetMdlByteOffset**](https://msdn.microsoft.com/library/windows/hardware/ff554533)
[**MmGetMdlPfnArray** ](https://msdn.microsoft.com/library/windows/hardware/ff554537) 
[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)
[**MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) 
 [ **MmPrepareMdlForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554660)








