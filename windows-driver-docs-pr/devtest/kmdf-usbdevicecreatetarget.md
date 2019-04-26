---
title: UsbDeviceCreateTarget ルール (kmdf)
description: UsbDeviceCreateTarget ルールでは、デバイス コンテキストでは現在 WDFUSBDEVICE オブジェクトがリーク中に複数 WDFUSBDEVICE オブジェクトが作成しないことを指定します。
ms.assetid: c2617c2b-553e-44fa-abd5-6bfe6d545612
ms.date: 05/21/2018
keywords:
- UsbDeviceCreateTarget ルール (kmdf)
topic_type:
- apiref
api_name:
- UsbDeviceCreateTarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be8603547204b01d95b7df25c4bfa19c36f42e38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354397"
---
# <a name="usbdevicecreatetarget-rule-kmdf"></a>UsbDeviceCreateTarget ルール (kmdf)


**UsbDeviceCreateTarget**ルールでは、デバイス コンテキストでは現在 WDFUSBDEVICE オブジェクトがリーク中に複数 WDFUSBDEVICE オブジェクトが作成しないことを指定します。

たとえば、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)イベント コールバック関数できます複数回ときに呼び出される、システム リソースを管理しようとメモリのさまざまなチャンクを割り当てる必要があります、ドライバー。 このような状況で、 [ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)イベント コールバック関数は、フレームワークが最初に呼び出された後に、メモリ リソースをマップ解除する*EvtDevicePrepareHardware*. *EvtDevicePrepareHardware*がし、再度呼び出されるドライバーがデバイスに割り当てられているメモリにアクセスできるように、リソースをマップします。 このルールは、ドライバーは、ターゲット WDFUSBDEVICE ことをまずを検証チェック**NULL**とはだけでなく新しいデバイスを作成し、前のハンドルを置き換えます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>UsbDeviceCreateTarget</strong>ルール。</p>
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

[**WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)
[**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)
 

 





