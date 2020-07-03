---
title: Init \_ registerinterrupt rule (ndis)
description: Init \_ registerinterrupt 規則は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生する割り込みの登録を元に戻す必要があることを指定します。NdisMRegisterInterruptEx が MiniportInitializeEx 中に少なくとも1回呼び出される場合は、NdisMDeregisterInterruptEx 関数を MiniportHaltEx で少なくとも1回呼び出す必要があります。
ms.assetid: f12cc1b9-396b-4351-ad13-c1750b54b709
ms.date: 05/21/2018
keywords:
- Init_RegisterInterrupt 規則 (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f92614b292233cffddb12bbdb4021da5d23d136
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918052"
---
# <a name="init_registerinterrupt-rule-ndis"></a>Init \_ registerinterrupt rule (ndis)


Init \_ registerinterrupt 規則は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生する割り込みの登録を元に戻す必要があることを指定します。

**NdisMRegisterInterruptEx**が**MiniportInitializeEx**中に少なくとも1回呼び出される場合は、 **NdisMDeregisterInterruptEx**関数を**miniporthaltex**で少なくとも1回呼び出す必要があります。

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Init_RegisterInterrupt</strong>規則を指定します。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex) 
[ **NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)
 

 





