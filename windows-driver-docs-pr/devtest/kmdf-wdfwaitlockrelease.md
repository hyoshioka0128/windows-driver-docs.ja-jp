---
title: WdfWaitlockRelease ルール (kmdf)
description: WdfWaitlockRelease ルールでは、KMDF イベントコールバック関数内で、Wdfwaitlockrelease と WdfWaitLockRelease の呼び出しが均衡の取れた方法で使用されることを指定します。
ms.assetid: 4ac60469-b9a3-4777-865b-f03d5a4da8ed
ms.date: 05/21/2018
keywords:
- WdfWaitlockRelease ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfWaitlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6757b856cd51a6802a6d23397c98f3bf7058a335
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839428"
---
# <a name="wdfwaitlockrelease-rule-kmdf"></a>WdfWaitlockRelease ルール (kmdf)


**Wdfwaitlockrelease**ルールでは、kmdf イベントコールバック関数内で、 [**Wdfwaitlockrelease**](https://msdn.microsoft.com/library/windows/hardware/ff551168)と[**wdfwaitlockrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)の呼び出しが均衡の取れた方法で使用されることを指定します。 KMDF イベントのコールバック関数から制御が戻ったときに、以前の**Wdfwaitlockacquire**の呼び出しで取得されたフレームワークのスピンロックオブジェクトをドライバーが保持することはできません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Wdfwaitlockrelease</strong>ルールを指定します。</p>
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

<a name="applies-to"></a>適用対象
----------

[**Wdfwaitlockacquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168) [ **Wdfwaitlockacquire**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)
 

 





