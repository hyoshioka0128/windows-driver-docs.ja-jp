---
title: IrqlKeDispatchLte ルール (wdm)
ms.assetid: 425a20ea-c9e3-45f4-a517-6bad9ab0de98
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeDispatchLte ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeDispatchLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22fe0d717046da2ab5a33b6c1338eff6396565df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582607"
---
# <a name="irqlkedispatchlte-rule-wdm"></a>IrqlKeDispatchLte ルール (wdm)


**IrqlKeDispatchLte**ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のカーネル ルーチンを呼び出すことを指定します&lt;= ディスパッチ\_レベル。

-   [**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)

-   [**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)

-   [**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)

-   [**KeFlushIoBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff552041)

-   [**KeInitializeDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552126)

-   [**KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)

-   [**KeInitializeTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff552173)

-   [**KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)

-   [**KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)

-   [**KeReadStateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553089)

-   [**KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)

-   [**KeReleaseMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553140)

-   [**KeRemoveEntryDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553163)

-   [**KeResetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553176)

-   [**KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)

-   [**KeSetTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553286)

-   [**KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020011) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeDispatchLte</strong>ルール。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)
[**KeClearEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff551980) 
 [ **KeInitializeDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552126)
[**KeInitializeSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff552150) 
[ **KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)
[**KeInitializeTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552173) 
 [**KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)
[**KeReadStateEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553089) 
 [ **KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)
[**KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140) 
 [ **KeRemoveEntryDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553163)
[**KeResetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553176) 
 [ **KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)
[**KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286) 
 [ **KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)
 

 





