---
title: WriteErrorLog ルール (ndis)
description: WriteErrorLog ルールでは、MiniportInitializeEx 関数で NdisMAllocateSharedMemory 関数が呼び出された場合、ドライバーは、割り当てが失敗した場合に NdisWriteErrorLogEntry も呼び出す必要があることを指定します。
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
ms.openlocfilehash: cc3f196f81ef90fba7b565cbae41aacec22b9cc8
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917838"
---
# <a name="writeerrorlog-rule-ndis"></a>WriteErrorLog ルール (ndis)


WriteErrorLog ルールでは、 *MiniportInitializeEx*関数で**NdisMAllocateSharedMemory**関数が呼び出された場合、ドライバーは、割り当てが失敗した場合に**NdisWriteErrorLogEntry**も呼び出す必要があることを指定します。

一般に、割り当てメモリ操作が失敗した場合は常に、ログにエラーエントリを記録することをお勧めします。 ほとんどの割り当て操作は、 *MiniportInitializeEx* callback 関数で行われます。 エラーをログに記録する方法の詳細については、次のコード例を参照してください。

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>writeerrorlog ログ</strong>ルールを指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 





