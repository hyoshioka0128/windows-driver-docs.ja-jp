---
title: DeviceInitAllocate ルール (kmdf)
description: DeviceInitAllocate ルールの PDO デバイスまたは制御デバイス オブジェクト、framework のデバイス オブジェクトの初期化 WdfDeviceCreate ドライバー呼び出しの前に、WdfPdoInitAllocate または WdfControlDeviceInitAllocate メソッドを呼び出す必要がありますを指定します。
ms.assetid: 81bad62a-4bc3-4e34-9634-2a980e1941e5
ms.date: 05/21/2018
keywords:
- DeviceInitAllocate ルール (kmdf)
topic_type:
- apiref
api_name:
- DeviceInitAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: daf83daef2501ad66da0e1225b4a0d07c8bdd47d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551387"
---
# <a name="deviceinitallocate-rule-kmdf"></a>DeviceInitAllocate ルール (kmdf)


**DeviceInitAllocate**ルールは、PDO デバイスまたはデバイスにコントロール オブジェクトは、framework デバイス オブジェクトの初期化メソッドを指定します[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)または[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)ドライバー呼び出しの前に呼び出す必要があります[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DeviceInitAllocate</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
 

 





