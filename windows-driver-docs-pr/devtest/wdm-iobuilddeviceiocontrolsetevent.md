---
title: IoBuildDeviceIoControlSetEvent ルール (wdm)
description: IoBuildDeviceIoControlSetEvent ルールでは、ドライバーを IoBuildDeviceIoControlRequest を呼び出す必要がありますを呼び出さないこと KeSetEvent、ドライバーは、呼び出し元が割り当てたで初期化イベント オブジェクトへのポインターを提供している場合を指定します。
ms.assetid: F9721484-3156-4AF5-8C60-AF68644E602D
ms.date: 05/21/2018
keywords:
- IoBuildDeviceIoControlSetEvent ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildDeviceIoControlSetEvent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08837c3b2b514113d433167af25ccfa978c445a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538246"
---
# <a name="iobuilddeviceiocontrolsetevent-rule-wdm"></a>IoBuildDeviceIoControlSetEvent ルール (wdm)


**IoBuildDeviceIoControlSetEvent**ルールの呼び出しをドライバーを指定します[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)を呼び出してはならない[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)ドライバーは、呼び出し元が割り当てたで初期化イベント オブジェクトへのポインターを提供します。 **KeSetEvent**この IRP のドライバーによって呼び出される必要はありません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildDeviceIoControlSetEvent</strong>ルール。</p>
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

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)
[**KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137) 
 [ **KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)
 

 





