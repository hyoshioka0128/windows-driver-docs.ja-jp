---
title: IoBuildFsdIrpSignalEventInCompletion2 ルール (wdm)
description: IoBuildFsdIrpSignalEventInCompletion2 ルールでは、KeSetEvent が Irp-PendingReturned フラグが設定され、完了ルーチンは、ローカルで作成された非同期 IRP の処理時に、完了のルーチンで呼び出される必要があることを指定します。
ms.assetid: 2077EB25-4EAE-4F76-BEB1-C637DA39C07D
ms.date: 05/21/2018
keywords:
- IoBuildFsdIrpSignalEventInCompletion2 ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildFsdIrpSignalEventInCompletion2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b346d4d388a71041832d8530b500243498860b75
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393942"
---
# <a name="iobuildfsdirpsignaleventincompletion2-rule-wdm"></a>IoBuildFsdIrpSignalEventInCompletion2 ルール (wdm)


**IoBuildFsdIrpSignalEventInCompletion2**ルールを指定する[ **KeSetEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)完了ルーチンで呼び出される必要があるときに、 **Irp&gt;PendingReturned**フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。

ここで完了ルーチンは呼び出されません。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>IoBuildFsdIrpSignalEventInCompletion2</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)
[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)
[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)
 

 





