---
title: IrqlIoApcLte ルール (wdm)
description: IrqlIoApcLte ルールでは、IRQL APC で実行されている場合にのみ、ドライバーが、次の I/O マネージャー ルーチンを呼び出すことを指定します\_レベル IoDeleteDeviceIoGetInitialStackIoRaiseHardErrorIoRaiseInformationalHardError します。
ms.assetid: 1f0b2b9c-f67c-4e34-b079-6a2769f62879
ms.date: 05/21/2018
keywords:
- IrqlIoApcLte ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlIoApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1b20874de85b9da332c67bef9032272ef3472f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530772"
---
# <a name="irqlioapclte-rule-wdm"></a>IrqlIoApcLte ルール (wdm)


**IrqlIoApcLte**ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次の I/O マネージャー ルーチンを呼び出すことを指定します&lt;APC を =\_レベル。

-   [**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)

-   [**IoGetInitialStack**](https://msdn.microsoft.com/library/windows/hardware/ff549247)

-   [**IoRaiseHardError**](https://msdn.microsoft.com/library/windows/hardware/ff549482)

-   [**IoRaiseInformationalHardError**](https://msdn.microsoft.com/library/windows/hardware/ff549488)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020009) [**チェック 0 xa のバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlIoApcLte</strong>ルール。</p>
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

[**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)
[**IoGetInitialStack**](https://msdn.microsoft.com/library/windows/hardware/ff549247)
[**IoRaiseHardError** ](https://msdn.microsoft.com/library/windows/hardware/ff549482)
 [ **IoRaiseInformationalHardError** ](https://msdn.microsoft.com/library/windows/hardware/ff549488)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





