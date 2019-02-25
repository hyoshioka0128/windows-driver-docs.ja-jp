---
title: IrqlDispatch ルール (wdm)
description: IrqlDispatch ルールでは、IRQL のディスパッチで実行されている場合にのみ、ドライバーが次の Ddi を呼び出すことを指定します\_レベル。
ms.assetid: f72d4f27-b488-4d0a-97b7-9cb40f00e346
ms.date: 05/21/2018
keywords:
- IrqlDispatch ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 853eb3fa48047e6694954849cd386bcb804f8d4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538258"
---
# <a name="irqldispatch-rule-wdm"></a>IrqlDispatch ルール (wdm)


**IrqlDispatch**ルールでは、IRQL で実行されている場合にのみ、ドライバーが次の Ddi を呼び出すことを指定します = ディスパッチ\_レベル。

-   [**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)

-   [**FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)

-   [**GetScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff546531)

-   [**IoAllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff548216)

-   [**IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)

-   [**IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)

-   [**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)

-   [**KeAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551921)

-   [**KeInsertByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552178)

-   [**KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)

-   [**KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)

-   [**KeRemoveByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553152)

-   [**KeRemoveDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553156)

-   [**PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**0 xa-チェックをバグします。IRQL\_いない\_少ない\_または\_等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) 、 [**チェック 0xC4 のバグします。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020003) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlDispatch</strong>ルール。</p>
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

 

<a name="applies-to"></a>適用対象
----------

[**AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)
[**AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575) 
 [ **BuildMdlFromScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff540686)
[**BuildScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff540689) 
 [ **FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917)
[**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)
[**FreeCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff546511) 
 [ **FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)
[**GetDmaAlignment** ](https://msdn.microsoft.com/library/windows/hardware/ff546530)
 [ **GetScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff546531)
[**IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224) 
[ **IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)
[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358) 
[ **IoWriteErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff550527)
[**KeInsertByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552178)
 [ **KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)
[**KeRemoveByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553152) 
 [ **KeRemoveDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553156)
[**MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402) 
 [ **PutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff559965)
[**PutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff559967) 
 [ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





