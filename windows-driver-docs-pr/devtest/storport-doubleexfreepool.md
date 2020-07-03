---
title: DoubleExFreePool ルール (storport)
description: このルールは、ドライバーが同じプールメモリブロックを2回解放しようとしないことを確認します。
ms.assetid: D7EAD257-02CA-418C-B67D-FADCB4F7A6C1
ms.date: 05/21/2018
keywords:
- DoubleExFreePool ルール (storport)
topic_type:
- apiref
api_name:
- DoubleExFreePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e64da7be8b0b394add3c1158c59b6cbefafcd40
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917747"
---
# <a name="doubleexfreepool-rule-storport"></a>DoubleExFreePool ルール (storport)


このルールは、ドライバーが同じプールメモリブロックを2回解放しようとしないことを確認します。

このルールは、最初に**Exfreepool**に渡されるメモリポインターを追跡します。 同じポインターが再び渡されると、ドライバーはルールに失敗します。 ドライバーが**Removeヘッドホン list**または**removeheadlist**を呼び出した場合、規則はに合格します。

**ドライバーモデル: Storport**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DoubleExFreePool</strong>規則を指定します。</p>
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

[**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 
[**Removeentrylist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeentrylist) 
[**Removeヘッドホンの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 





