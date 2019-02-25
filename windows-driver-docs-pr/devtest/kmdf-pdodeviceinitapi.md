---
title: PdoDeviceInitAPI ルール (kmdf)
description: PdoDeviceInitAPI ルールは、その WdfPdoInitAllocate とすべての他のデバイス オブジェクトの初期化を設定する、WDFDEVICE Ddi を指定します\_(PDO) 物理デバイス オブジェクトの初期化構造体は、ドライバーの前に呼び出す必要がありますの WdfDeviceCreate を呼び出し、。PDO します。
ms.assetid: 6a2e6e82-7fac-4366-a46d-1bd80d3bf92e
ms.date: 05/21/2018
keywords:
- PdoDeviceInitAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- PdoDeviceInitAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1273d9f38eab54ef8d2ad00619282d8e99cb24c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551392"
---
# <a name="pdodeviceinitapi-rule-kmdf"></a>PdoDeviceInitAPI ルール (kmdf)


**PdoDeviceInitAPI**ルールを指定する[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)とすべての他のデバイス オブジェクトの初期化を設定する Ddi、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)ドライバー呼び出しの前に、物理デバイス オブジェクト (PDO) を呼び出す必要がありますの構造体[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)PDO します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PdoDeviceInitAPI</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
[**WdfDeviceInitAssignSDDLString** ](https://msdn.microsoft.com/library/windows/hardware/ff546035) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) 
 [ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546057)
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546066) 
 [ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071)
[**WdfDeviceInitSetCharacteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff546074)
 [ **WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)
[**WdfDeviceInitSetDeviceType** ](https://msdn.microsoft.com/library/windows/hardware/ff546090)
 [ **WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)
[**WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107) 
 [ **WdfDeviceInitSetIoInCallerContextCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546119) 
 [ **WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)
[**WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135) 
[ **WdfDeviceInitSetPowerInrush**](https://msdn.microsoft.com/library/windows/hardware/ff546142)
[**WdfDeviceInitSetPowerNotPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546147)
 [ **WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766) 
 [ **WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774)
[**WdfDeviceInitSetPowerPolicyOwnership** ](https://msdn.microsoft.com/library/windows/hardware/ff546776) 
[ **WdfDeviceInitSetRequestAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff546786)
[**WdfFdoRetrieveNextStaticChild**](https://msdn.microsoft.com/library/windows/hardware/ff547293) 
 [ **WdfPdoInitAddCompatibleID**](https://msdn.microsoft.com/library/windows/hardware/ff548776)
[{11**](https://msdn.microsoft.com/library/windows/hardware/ff548805)
 

 





