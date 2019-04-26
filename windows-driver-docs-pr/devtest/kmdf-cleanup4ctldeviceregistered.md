---
title: Cleanup4CtlDeviceRegistered ルール (kmdf)
description: Cleanup4CtlDeviceRegistered ルールは、プラグ アンド プレイ (PnP) ドライバーは、コントロールのデバイス オブジェクトの WdfDeviceCreate を呼び出し、ドライバー登録する必要があります、必要なイベントのコールバック関数のいずれかを指定します。
ms.assetid: f439ec36-f7af-46e5-8ddd-11e444bf36da
ms.date: 05/21/2018
keywords:
- Cleanup4CtlDeviceRegistered ルール (kmdf)
topic_type:
- apiref
api_name:
- Cleanup4CtlDeviceRegistered
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e18af64c81953045854b429c117b82e07f814c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340399"
---
# <a name="cleanup4ctldeviceregistered-rule-kmdf"></a>Cleanup4CtlDeviceRegistered ルール (kmdf)


**Cleanup4CtlDeviceRegistered**ルールを指定するプラグ アンド プレイ (PnP) ドライバーを呼び出す場合[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)制御デバイス オブジェクト、ドライバーが必要があります必要なイベントのコールバック関数の 1 つを登録します。

イベントのコールバック関数には、次のいずれかを指定できます。

[*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)で、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)制御デバイス用の構造 - または - [ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)で、 [ **WDF\_PNPPOWER\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff552416)構造体

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Cleanup4CtlDeviceRegistered</strong>ルール。</p>
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









