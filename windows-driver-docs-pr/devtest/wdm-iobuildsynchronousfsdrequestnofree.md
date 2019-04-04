---
title: IoBuildSynchronousFsdRequestNoFree ルール (wdm)
description: IoBuildSynchronousFsdRequestNoFree ルールでは、ドライバーを IoBuildSynchronousFsdRequest を呼び出す必要があります IoFreeIrp を呼び出さないことを指定します。
ms.assetid: 516D6B53-866D-477D-AB9C-6E44BB285BA8
ms.date: 05/21/2018
keywords:
- IoBuildSynchronousFsdRequestNoFree ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildSynchronousFsdRequestNoFree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20f99407c053ba781781bd1faa10a958ac6ca35b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553926"
---
# <a name="iobuildsynchronousfsdrequestnofree-rule-wdm"></a>IoBuildSynchronousFsdRequestNoFree ルール (wdm)


**IoBuildSynchronousFsdRequestNoFree**ルールの呼び出しをドライバーを指定します[ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)を呼び出してはならない[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)します。

**IoBuildSynchronousFsdRequestNoFree**ルールは、報告される[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)この IRP を呼び出すことはできません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildSynchronousFsdRequestNoFree</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)
[**IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)
 

 





