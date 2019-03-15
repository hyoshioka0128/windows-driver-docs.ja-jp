---
title: CtlDeviceFinishInitDrEntry ルール (kmdf)
description: CtlDeviceFinishInitDrEntry ルールでは、こと、ドライバーは、DriverEntry コールバック関数で、制御デバイス オブジェクトを作成する場合に呼び出す必要があります WdfControlFinishInitializing、EvtDriverDeviceAdd から終了前に、デバイスが作成された後を指定しますコールバック関数。 このルールは、非 PnP ドライバーには適用されません。
ms.assetid: b6470bc1-c4db-4b46-b83b-edcf4da56087
ms.date: 05/21/2018
keywords:
- CtlDeviceFinishInitDrEntry ルール (kmdf)
topic_type:
- apiref
api_name:
- CtlDeviceFinishInitDrEntry
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c50b673a8d99adbd853cd7ea70bc399451486bc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548578"
---
# <a name="ctldevicefinishinitdrentry-rule-kmdf"></a>CtlDeviceFinishInitDrEntry ルール (kmdf)


CtlDeviceFinishInitDrEntry ルール指定するドライバーの制御デバイス オブジェクトを作成する場合、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)コールバック関数を呼び出す必要があります[ **WdfControlFinishInitializing** ](https://msdn.microsoft.com/library/windows/hardware/ff545854)から終了前に、デバイスが作成された後、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 このルールは、非 PnP ドライバーには適用されません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CtlDeviceFinishInitDrEntry</strong>ルール。</p>
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

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfControlFinishInitializing**](https://msdn.microsoft.com/library/windows/hardware/ff545854)
[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
 

 




