---
title: DeleteDevice ルール (wdm)
description: DeleteDevice ルールは、ドライバーが IoDeleteDevice への呼び出し後、デバイス オブジェクトを維持するには、I/O マネージャーまたは PnP マネージャーに依存する必要がありますを指定します。
ms.assetid: C7068AD1-C9F4-4BB0-8964-24FFB4658AF6
ms.date: 05/21/2018
keywords:
- DeleteDevice ルール (wdm)
topic_type:
- apiref
api_name:
- DeleteDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb4b84b429e319d2446b0188a18500932f757d24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558199"
---
# <a name="deletedevice-rule-wdm"></a>DeleteDevice ルール (wdm)


**DeleteDevice**ルールは、ドライバーが呼び出しの後に、デバイス オブジェクトを維持するには、I/O マネージャーまたは PnP マネージャーに依存する必要がありますを指定します[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)します。

ドライバーを呼び出す必要があります[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)下位のドライバーが返された後です。 これは、推奨される動作です。 このルールは、ドライバーの FDO と FIDO に適用されます。

処理するときに、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)要求、のみ、ドライバーを呼び出す[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)後[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)が返されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DeleteDevice</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





