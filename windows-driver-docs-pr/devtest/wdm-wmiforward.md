---
title: WmiForward ルール (wdm)
description: WmiForward ルールでは、転送が必要な場合に、ドライバーが WMI のマイナー Irp を転送する必要がありますを指定します。
ms.assetid: c62f37d2-ebd5-4705-9590-d1bf17137802
ms.date: 05/21/2018
keywords:
- WmiForward ルール (wdm)
topic_type:
- apiref
api_name:
- WmiForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d81fb6cc41678a0a0c5d0578cc2d7a58cdcae2cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573818"
---
# <a name="wmiforward-rule-wdm"></a>WmiForward ルール (wdm)


**WmiForward**ルールでは、ドライバーを転送する必要がありますを指定します[ **WMI マイナー Irp** ](https://msdn.microsoft.com/library/windows/hardware/ff566361)転送が必要な場合。

具体的には、ドライバーを呼び出すと[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)の値、 *IrpDisposition*パラメーターが**IrpForward**、ドライバーを呼び出す必要があります[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)ディスパッチから戻る前に、IRP を転送するにはルーチンです。

このルールは、バス ドライバーには適用されません。

A *WMI マイナー IRP*は、 [ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813) WMI マイナー関数コードで要求します。

WMI のマイナー Irp の処理に関する詳細については、次を参照してください[ **WDM ドライバーの要件を WMI**](https://msdn.microsoft.com/library/windows/hardware/ff566370)、 [ **WMI 要求の処理**](https://msdn.microsoft.com/library/windows/hardware/ff546968)、 。[**Windows Management Instrumentation ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff565794)、および[ **WMI ライブラリ サポート ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff566359)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WmiForward</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)参照してください。
--------

[**WDM ドライバーの要件を WMI**](https://msdn.microsoft.com/library/windows/hardware/ff566370)
[**WMI 要求を処理して**](https://msdn.microsoft.com/library/windows/hardware/ff546968)
[**WMI ライブラリのサポートルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff566359)
 

 





