---
title: WdfSpinlockRelease ルール (kmdf)
description: WdfSpinlockRelease ルールでは、KMDF イベントのコールバック関数内でバランスの取れた方法で WdfSpinLockAcquire および WdfSpinlockRelease への呼び出しが使用されることを指定します。
ms.assetid: ecb07a60-d55c-4990-aeef-5c880c13c2a1
ms.date: 05/21/2018
keywords:
- WdfSpinlockRelease ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfSpinlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c76773655a55fdc6cb7f2ea4e52d84299217ecea
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392804"
---
# <a name="wdfspinlockrelease-rule-kmdf"></a>WdfSpinLockRelease ルール (kmdf)


**WdfSpinLockRelease**への呼び出し規則を指定[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))と**WdfSpinLockRelease**使用は、バランスの取れたでKMDF イベントのコールバック関数内で。 ドライバーでは、以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクトは保持しないようにする、KMDF イベントのコールバック関数が戻るとき**WdfSpinLockAcquire**します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WdfSpinLockRelease</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))
[**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))
 

 





