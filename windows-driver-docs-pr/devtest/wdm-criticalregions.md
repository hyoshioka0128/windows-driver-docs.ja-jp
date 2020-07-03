---
title: CriticalRegions ルール (wdm)
description: CriticalRegions 規則は、ドライバーが KeLeaveCriticalRegion を呼び出す前に KeEnterCriticalRegion を呼び出す必要があることを指定します。また、KeEnterCriticalRegion の後続の呼び出しの前に、ドライバーが KeLeaveCriticalRegion を呼び出します。 (入れ子になった呼び出しは許可されます。)。
ms.assetid: 5976e24b-ca1c-440e-97c8-ccc2015d1172
ms.date: 05/21/2018
keywords:
- CriticalRegions ルール (wdm)
topic_type:
- apiref
api_name:
- CriticalRegions
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 777906808e417767c558f5d675a6f160d6eabbe6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916411"
---
# <a name="criticalregions-rule-wdm"></a>CriticalRegions ルール (wdm)


**CriticalRegions**規則は、ドライバーが[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)を呼び出す前に[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出す必要があることを指定します。また、 **KeEnterCriticalRegion**の後続の呼び出しの前に、ドライバーが**KeLeaveCriticalRegion**を呼び出します。 (入れ子になった呼び出しが許可されます)。

このルールは、ドライバーが**KeLeaveCriticalRegion**を呼び出して、制御が戻る前に通常のカーネル非同期プロシージャ呼び出し (apc) の配信を再び有効にすることも指定します。

**KeEnterCriticalRegion**と**KeLeaveCriticalRegion**の WDK ドキュメントでは、これらの関数の呼び出し元が IRQL = APC レベルで実行できることについて説明して &lt; \_ います。 このような状況では、このルールによってベストプラクティスの推奨事項が適用されます。

**ドライバーモデル: WDM**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00040003) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>CriticalRegions</strong>規則を指定します。</p>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking#ddi-compliance-checking-additional" data-raw-source="[DDI compliance checking (additional)](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking#ddi-compliance-checking-additional)">DDI 準拠の確認 (追加)</a> ] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**ExEnterCriticalRegionAndAcquireResourceExclusive**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn308550(v=vs.85)) 
[**ExReleaseResourceAndLeaveCriticalRegion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn308551(v=vs.85)) 
[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 
[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)
 

 





