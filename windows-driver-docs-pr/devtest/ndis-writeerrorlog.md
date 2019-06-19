---
title: WriteErrorLog ルール (ndis)
description: WriteErrorLog ルールでは、ある NdisMAllocateSharedMemory 関数は MiniportInitializeEx 関数で呼び出されると、ドライバー呼び出す必要がありますも NdisWriteErrorLogEntry 割り当てに失敗した場合を指定します。
ms.assetid: b626f25a-3101-4c0a-b0a9-fef6ce964055
ms.date: 05/21/2018
keywords:
- WriteErrorLog ルール (ndis)
topic_type:
- apiref
api_name:
- WriteErrorLog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2824b5870658c69f5828b2b6313d18eca6e59fd7
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161558"
---
# <a name="writeerrorlog-rule-ndis"></a>WriteErrorLog ルール (ndis)


WriteErrorLog ルールで指定された場合、 **NdisMAllocateSharedMemory**関数が呼び出されます、 *MiniportInitializeEx*関数の場合、ドライバーは呼び出す必要がありますも**NdisWriteErrorLogEntry**割り当てに失敗した場合。

一般は割り当てメモリ操作が失敗したときに、エラーのエントリをログに記録することをお勧めします。 ほとんどの割り当て操作が発生する、 *MiniportInitializeEx*コールバック関数。 エラー ログに記録する方法の詳細については、次のコード例を参照してください。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="example"></a>例
-------

```
// an example of how to log an error if memory allocation fails PVOID p;
NdisMAllocateSharedMemory(par1, par2, par3, &p, ...);
if (p == NULL)
{
 NdisWriteErrorLogEntry("Memory allocation failed");
}
```

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WriteErrorLog</strong>ルール。</p>
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

 

 





