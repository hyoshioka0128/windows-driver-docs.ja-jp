---
title: PagedCodeAtPowerTrans ルール (wdm)
description: PagedCodeAtPowerTrans ルールでは、ドライバーがページングを呼び出さないことを指定します\_システム IRP の応答中にコード\_MJ\_POWER Irp (IRP\_MN\_設定\_電源) とデバイスの IRP に\_MJ\_POWER Irp (IRP\_MN\_設定\_POWER)。
ms.assetid: D94B0E13-9640-4FBF-B1E7-AF8DFED42542
ms.date: 05/21/2018
keywords:
- PagedCodeAtPowerTrans ルール (wdm)
topic_type:
- apiref
api_name:
- PagedCodeAtPowerTrans
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f885ae946929c51dfdfa4634c82a864feefff77a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368017"
---
# <a name="pagedcodeatpowertrans-rule-wdm"></a>PagedCodeAtPowerTrans ルール (wdm)


**PagedCodeAtPowerTrans**ルールでは、ドライバーを呼び出さないことを指定します[**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)システム IRP の応答中に\_MJ\_電源 Irp (IRP\_MN\_設定\_電源) とデバイスの IRP に\_MJ\_POWER Irp (IRP\_MN\_設定\_POWER)。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PagedCodeAtPowerTrans</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ページングされた\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)
 

 





