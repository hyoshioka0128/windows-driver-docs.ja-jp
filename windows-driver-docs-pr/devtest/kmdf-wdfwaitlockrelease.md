---
title: WdfWaitlockRelease ルール (kmdf)
description: WdfWaitlockRelease ルールでは、KMDF イベントのコールバック関数内でバランスの取れた方法で WdfWaitLockAcquire および WdfWaitLockRelease への呼び出しが使用されることを指定します。
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
ms.openlocfilehash: 0bb9b16e95bc34b8115c705349d9f19afa0b5bb3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392786"
---
# <a name="wdfwaitlockrelease-rule-kmdf"></a>WdfWaitlockRelease ルール (kmdf)


**WdfWaitlockRelease**への呼び出し規則を指定[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)と[ **WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease) KMDF イベントのコールバック関数内でバランスの取れた方法で使用されます。 ドライバーでは、以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクトは保持しないようにする、KMDF イベントのコールバック関数が戻るとき**WdfWaitLockAcquire**します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WdfWaitlockRelease</strong>ルール。</p>
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

[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)
[**WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease)
 

 





