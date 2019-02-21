---
title: ControlDeviceDeleted ルール (kmdf)
description: ControDeviceDeleted ルールでは、PnP ドライバーでは、コントロールのデバイス オブジェクトを作成する場合、ドライバーはドライバーがアンロードする前に、クリーンアップのコールバック関数のいずれかで制御デバイス オブジェクトを削除する必要があるを指定します。
ms.assetid: 869f1c1c-8a9f-4e0b-bcbb-386e93663567
ms.date: 05/21/2018
keywords:
- ControlDeviceDeleted ルール (kmdf)
topic_type:
- apiref
api_name:
- ControlDeviceDeleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08a58b94352f3c5e2171940cb9ea553da921d8ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548798"
---
# <a name="controldevicedeleted-rule-kmdf"></a>ControlDeviceDeleted ルール (kmdf)


ControDeviceDeleted ルールでは、PnP ドライバーでは、コントロールのデバイス オブジェクトを作成する場合、ドライバーはドライバーがアンロードする前に、クリーンアップのコールバック関数のいずれかで制御デバイス オブジェクトを削除する必要があるを指定します。

FDO またはフィルター ドライバーを呼び出す場合[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)制御デバイス オブジェクト、ドライバーが呼び出す必要があります[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)のWDFDEVICE オブジェクト、WDFDEVICE オブジェクトの破棄のコールバック関数のドライバーの cleanup callback 関数から制御デバイス オブジェクト、または[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)イベント コールバック関数。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ControlDeviceDeleted</strong>ルール。</p>
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
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
 

 





