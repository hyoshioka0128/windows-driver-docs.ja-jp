---
title: PowerUpFail ルール (wdm)
description: PowerUpFail ルールを指定、FDO または FIDO ドライバーは IRP を失敗しません\_MN\_設定\_POWER 要求、デバイスの電源を入れるとき。
ms.assetid: 48998C82-91F6-42F9-AF7A-4E5ECAB823E1
ms.date: 05/21/2018
keywords:
- PowerUpFail ルール (wdm)
topic_type:
- apiref
api_name:
- PowerUpFail
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0108043d9eb4e54d675ebcc1db60febed08f9186
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370784"
---
# <a name="powerupfail-rule-wdm"></a>PowerUpFail ルール (wdm)


PowerUpFail ルールを指定、FDO または FIDO ドライバーは IRP を失敗しません\_MN\_設定\_POWER 要求、デバイスの電源を入れるとき。

このルールは、FDO および FIDO ドライバーのみに適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PowerUpFail</strong>ルール。</p>
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

[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)
 

 





