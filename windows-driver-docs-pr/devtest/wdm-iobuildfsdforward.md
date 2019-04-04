---
title: IoBuildFsdForward ルール (wdm)
description: IoBuildFsdForward ルールでは、ドライバーを呼び出す保留または PoCallDriver IRP が IoBuildAsynchronousFsdRequest への呼び出しによって生成された場合は、前に完了ルーチンを設定する必要がありますを指定します。
ms.assetid: 89F221D5-3B04-40B9-BB9F-5F4C97FC2BDB
ms.date: 05/21/2018
keywords:
- IoBuildFsdForward ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildFsdForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64afb3629625311e5887f4df4315908115691f16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558864"
---
# <a name="iobuildfsdforward-rule-wdm"></a>IoBuildFsdForward ルール (wdm)


**IoBuildFsdForward**ルールでは、ドライバーを呼び出す前に完了ルーチンを設定する必要がありますを指定します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) IRP がへの呼び出しによって生成される場合[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildFsdForward</strong>ルール。</p>
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

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
 [ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





