---
title: IrqlPsPassive ルール (wdm)
ms.assetid: db84c945-7695-4691-8294-095bbc74ef8a
ms.date: 05/21/2018
description: ''
keywords:
- IrqlPsPassive ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlPsPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72395a5e14dd7aca46bcda6222244c47c4fb7fcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839909"
---
# <a name="irqlpspassive-rule-wdm"></a>IrqlPsPassive ルール (wdm)


**IrqlPsPassive**規則は、IRQL = パッシブ\_レベルで実行されている場合にのみ、ドライバーが次の[**プロセス構造ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことを指定します。

-   [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)

-   [**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psgetversion)

-   [**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)

-   [**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)

-   [**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)

-   [**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0002001C) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlPsPassive</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
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

[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)
[**Psgetversion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psgetversion)
[**pssetcreateprocessnotifyルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)
[**Pssetcreatethreadnotifyルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)
[**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)
[**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread)
 

 





