---
title: StorPortMSILock ルール (storport)
description: ミニポート ドライバーにのみの場合、メッセージの MSI スピン ロックの取得に必要なポートの InterruptSynchronizationMode メンバー\_構成\_に設定されている情報 (Storport) 構造体InterruptSynchronizePerMessage します。
ms.assetid: 99C45ADB-AFCC-4B9E-8EB9-DBD7C7F6D800
ms.date: 05/21/2018
keywords:
- StorPortMSILock ルール (storport)
topic_type:
- apiref
api_name:
- StorPortMSILock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50116c8aeefd5dac4dbe7f37ad8b737d1f7a3953
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532006"
---
# <a name="storportmsilock-rule-storport"></a>StorPortMSILock ルール (storport)


のみの場合、メッセージの MSI スピン ロックを取得するミニポート ドライバーが必要、 **InterruptSynchronizationMode**のメンバー、 [**ポート\_構成\_情報 (Storport)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)構造に設定されている**InterruptSynchronizePerMessage**します。 このルールへの呼び出しを検証[ **StorPortAcquireMSISpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff567023)同期モードの場合のみ行われます**InterruptSynchronizePerMessage**します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortMSILock</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 





