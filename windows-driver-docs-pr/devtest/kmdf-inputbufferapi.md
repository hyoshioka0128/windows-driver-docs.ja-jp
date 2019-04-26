---
title: InputBufferAPI ルール (kmdf)
ms.assetid: 11388ffa-633d-4129-9693-a351ec8b0735
ms.date: 05/21/2018
description: ''
keywords:
- InputBufferAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- InputBufferAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ec64e7b21bbc4d973de61f1f16252bad3e76a21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340282"
---
# <a name="inputbufferapi-rule-kmdf"></a>InputBufferAPI ルール (kmdf)


**InputBufferAPI**ルールでは、バッファー取得のための正しい Ddi で使用されることを指定します、 [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)コールバック関数。 内で、 *EvtIoRead*コールバック関数では、次の Ddi はバッファー取得のため呼び出すことができません。

[**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
[**WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)
[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>InputBufferAPI</strong>ルール。</p>
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

[**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)
[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)
[**WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)








