---
title: IrqlExApcLte2 ルール (wdm)
description: IrqlExApcLte2 ルールでは、IRQL APC でのみ、ドライバーが、次のルーチンを呼び出すことを指定します\_レベル。
ms.assetid: 5800ec58-2084-4092-9614-dd631458c7dd
ms.date: 05/21/2018
keywords:
- IrqlExApcLte2 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlExApcLte2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5f72e8bca9cbf4561779374b971470a48e1d238
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359442"
---
# <a name="irqlexapclte2-rule-wdm"></a>IrqlExApcLte2 ルール (wdm)


**IrqlExApcLte2**ルールでは、IRQL でのみ、ドライバーが、次のルーチンを呼び出すことを指定します&lt;APC を =\_レベル。

-   [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)

-   [**CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)

-   [**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)

-   [**ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)

-   [**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)

-   [**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)

-   [**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)

-   [**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)

-   [**ExRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545534)

-   [**ExSetTimerResolution**](https://msdn.microsoft.com/library/windows/hardware/ff545614)

-   [**ExUnregisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545649)

-   [**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

-   [**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020006) [**チェック 0 xa のバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlExApcLte2</strong>ルール。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)
[**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921)
[**CmUnRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541928) 
 [ **ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)
[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309) 
 [ **ExRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545534)
[**ExSetTimerResolution** ](https://msdn.microsoft.com/library/windows/hardware/ff545614)
 [ **ExUnregisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545649)
[**ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876) 
 [**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)
 

 





