---
title: IrqlKeApcLte2 ルール (wdm)
ms.assetid: 585d741d-543f-421b-be48-28f48d68fc4d
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeApcLte2 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeApcLte2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad1d8b122e6a1f81028c1119ed4c4f5901fdc5ff
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968557"
---
# <a name="irqlkeapclte2-rule-wdm"></a>IrqlKeApcLte2 ルール (wdm)


**IrqlKeApcLte2**規則は、ドライバーが IRQL = APC レベルで実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定し &lt; \_ ます。

-   [**KeAreAllApcsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keareallapcsdisabled)

-   [**KeAreApcsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keareapcsdisabled)

-   [**KeDeregisterNmiCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisternmicallback)

-   [**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

-   [**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)

-   [**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)

-   [**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)

-   [**KeRegisterNmiCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisternmicallback)

**ドライバーモデル: WDM**

**このルールでバグチェックが見つかりました**:[**バグチェック 0XC4: ドライバー \_ 検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00020010)


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlKeApcLte2</strong>規則を指定します。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**KeDeregisterNmiCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisternmicallback) 
[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 
[**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion) 
[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 
[**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion) 
[**KeRegisterNmiCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisternmicallback)
 

 





