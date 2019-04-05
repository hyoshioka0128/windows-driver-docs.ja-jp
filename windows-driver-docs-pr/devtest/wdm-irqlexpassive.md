---
title: IrqlExPassive ルール (wdm)
description: IrqlExPassive ルールでは、ドライバーが IRQL パッシブにのみ、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します\_レベルExCreateCallbackExIsProcessorFeaturePresentExRaiseAccessViolationExRaiseDatatypeMisalignmentExRaiseStatusExUuidCreateThe IrqlExPassive ルールも指定します、ドライバーでは、IRQL APC で ExRaiseStatus が呼び出す\_レベル。
ms.assetid: 92d73bd9-ce79-4be8-9ea2-a5aef2ea6edb
ms.date: 05/21/2018
keywords:
- IrqlExPassive ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlExPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6a2c27b1b3529d4929491e8d9a01959149224cda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549933"
---
# <a name="irqlexpassive-rule-wdm"></a>IrqlExPassive ルール (wdm)


**IrqlExPassive**ルールでは、ドライバーが IRQL でのみ、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します = パッシブ\_レベル。

-   [**ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)

-   [**ExIsProcessorFeaturePresent**](https://msdn.microsoft.com/library/windows/hardware/ff545442)

-   [**ExRaiseAccessViolation**](https://msdn.microsoft.com/library/windows/hardware/ff545509)

-   [**ExRaiseDatatypeMisalignment**](https://msdn.microsoft.com/library/windows/hardware/ff545524)

-   [**ExRaiseStatus**](https://msdn.microsoft.com/library/windows/hardware/ff545529)

-   [**ExUuidCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545658)

**IrqlExPassive**もルールでは、ドライバーを呼び出すことを指定します[ **ExRaiseStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff545529) IRQL で&lt;APC を =\_レベル。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020008) [**チェック 0 xa のバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlExPassive</strong>ルール。</p>
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



<a name="applies-to"></a>適用対象
----------

[**ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)
[**ExIsProcessorFeaturePresent**](https://msdn.microsoft.com/library/windows/hardware/ff545442)
[**ExRaiseAccessViolation**](https://msdn.microsoft.com/library/windows/hardware/ff545509) 
 [ **ExRaiseDatatypeMisalignment**](https://msdn.microsoft.com/library/windows/hardware/ff545524)
[**ExRaiseStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff545529) 
 [ **ExUuidCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545658)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)








