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
ms.openlocfilehash: 2c577c76afc3158396757a248bc5e0d86a0c9f2b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392068"
---
# <a name="irqlpspassive-rule-wdm"></a>IrqlPsPassive ルール (wdm)


**IrqlPsPassive**ルールでは、ドライバーが、次を呼び出すことを指定します[**構造の処理ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) IRQL でその実行はときにのみ = パッシブ\_レベル:

-   [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)

-   [**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psgetversion)

-   [**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)

-   [**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)

-   [**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutine)

-   [**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psterminatesystemthread)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x0002001C) |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>IrqlPsPassive</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)
[**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psgetversion)
[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine) 
 [ **PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)
[**PsSetLoadImageNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutine) 
 [ **PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psterminatesystemthread)
 

 





