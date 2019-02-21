---
title: IoBuildDeviceControlNoFree ルール (wdm)
description: IoBuildDeviceControlNoFree ルールでは、ドライバーを IoBuildDeviceIoControlRequest を呼び出す必要があります IoFreeIrp を呼び出さないことを指定します。
ms.assetid: 36DAB9A8-2B6F-43EE-86CC-97B66FE0AEB8
ms.date: 05/21/2018
keywords:
- IoBuildDeviceControlNoFree ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildDeviceControlNoFree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4cd089852424a3945455bb7c84aa57ad8c0585f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553812"
---
# <a name="iobuilddevicecontrolnofree-rule-wdm"></a>IoBuildDeviceControlNoFree ルール (wdm)


**IoBuildDeviceControlNoFree**ルールの呼び出しをドライバーを指定します[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)を呼び出してはならない[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)します。

呼び出すドライバー [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)を呼び出してはならない[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113) I/O マネージャーは、これらを解放するため後の同期の Irp [ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)が呼び出されました。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildDeviceControlNoFree</strong>ルール。</p>
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

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)
 

 





