---
title: AddDevice ルール (wdm)
description: AddDevice ルールでは、ドライバーの AddDevice ルーチンが IoCreateDevice を呼び出した後にだけ IoAttachDeviceToDeviceStack を呼び出すことを指定します。
ms.assetid: 6379633a-194f-45b8-8c21-85eecf300aeb
ms.date: 05/21/2018
keywords:
- AddDevice ルール (wdm)
topic_type:
- apiref
api_name:
- AddDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 792ce1017eed0b28287be8a4c5b8a07f7a998fd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529388"
---
# <a name="adddevice-rule-wdm"></a>AddDevice ルール (wdm)


**AddDevice**ルールを指定するドライバーの[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンの呼び出し[ **IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)呼び出した後のみ[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)します。

このルールは、ドライバーにのみ適用されます、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

このルールは、ドライバーを呼び出すことは検証されません**IoCreateDevice**または**IoAttachDeviceToDeviceStack**への呼び出しは監視されません[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407).

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>AddDevice</strong>ルール。</p>
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

[**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)
[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)
 

 





