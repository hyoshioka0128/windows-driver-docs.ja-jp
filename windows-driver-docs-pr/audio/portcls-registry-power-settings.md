---
title: PortCls レジストリの電源設定
description: このトピックでは、Windows 8 の PortCls レジストリ電源設定について説明します。
ms.assetid: 148D044E-B736-4526-BDC5-2C180A590C21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 434a1e10747edb83b8deb74a14d9b45bc2257f4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574431"
---
# <a name="portcls-registry-power-settings"></a>PortCls レジストリの電源設定


このトピックでは、Windows 8 の PortCls レジストリ電源設定について説明します。

Windows 8 で (PortCls) ミニポート ドライバーで使用できますのレジストリ値、ドライバーのレジストリ キーには、次の。

-   PortCls にアイドル状態の電源管理が可能かどうかを判断します。

-   高パフォーマンス モードではなく、バッテリの保護モードのアイドル タイムアウト値を確認します。

Windows 8 の既定値は PortCls を使用して、電源マネージャーを使用した「デバイスがアイドル状態」検出の場合、実行時の電源のフレームワークでは、電源が必要でなくなったことを示しますを登録するかどうかを決定する電源設定です。 電源設定のプロファイルの記述に使用されるパラメーターの定義は次のとおりです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ値</th>
<th align="left">データ型</th>
<th align="left">既定値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ConservationIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0 秒のタイムアウト。</td>
</tr>
<tr class="even">
<td align="left">IdlePowerState</td>
<td align="left">REG_BINARY</td>
<td align="left">3 (D3)
<p>有効な値 :</p>
1-D1 2 - D2 3 - D3</td>
<td align="left">電源が不要になったときに、デバイスが入力されます電源の状態を指定します。</td>
</tr>
<tr class="odd">
<td align="left">PerformanceIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0 秒のタイムアウト。</td>
</tr>
</tbody>
</table>

 

次の Windows レジストリのフラグメントでは、電源設定の情報を提供するために使用されている構文を示します。

``` syntax
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4D36E96C-E325-11CE-BFC1-08002BE10318}\0000\PowerSettings]
"ConservationIdleTime"=hex:1e,00,00,00
"PerformanceIdleTime"=hex:00,00,00,00
“IdlePowerState”=hex:03,00,00,00
```

上記のコードの"1 e"の場合は、16 進数 (16 進数) 値を示しています、 *ConservationIdleTime*、し、これは 30 秒のアイドル タイムアウトに相当します。 16 進値「0」の表示の*PerformanceIdleTime*アイドル状態の管理が無効になっていることを意味します。 に対して表示される「03」の値、 *IdlePowerState* power が不要になったときにこの電源設定のプロファイルに関連付けられているデバイスは D3 電源の状態を入力する、ことを意味します。

 

 




