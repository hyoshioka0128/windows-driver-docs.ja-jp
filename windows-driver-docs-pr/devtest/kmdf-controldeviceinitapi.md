---
title: ControlDeviceInitAPI ルール (kmdf)
description: ControlDeviceInitAPI ルールは、その WdfControlDeviceInitAllocate とすべての他のデバイス オブジェクトの初期化を設定する、WDFDEVICE Ddi を指定します\_制御装置の INIT 構造は、コントロールの WdfDeviceCreate する前に呼び出す必要があります。デバイスです。
ms.assetid: 136ee6d8-d104-4ae8-a3f7-d93179808e29
ms.date: 05/21/2018
keywords:
- ControlDeviceInitAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- ControlDeviceInitAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 71e5dfe6f21d67fecf0a6200dc749f38ef92e3f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573050"
---
# <a name="controldeviceinitapi-rule-kmdf"></a>ControlDeviceInitAPI ルール (kmdf)


ControlDeviceInitAPI ルールを指定する[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)とすべての他のデバイス オブジェクトの初期化を設定する Ddi、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)制御デバイスは、前に呼び出す必要がありますの構造体[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)制御デバイスです。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ControlDeviceInitAPI</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfControlDeviceInitSetShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff545847) 
 [ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)
[**WdfDeviceInitSetCharacteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff546074) 
 [ **WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)
[**WdfDeviceInitSetExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff546097) 
 [ **WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)
[**WdfDeviceInitSetIoInCallerContextCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546119) 
[ **WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)
[**WdfDeviceInitSetRequestAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff546786)
 

 





