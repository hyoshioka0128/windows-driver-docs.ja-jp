---
title: PortCls レジストリの電源設定
description: このトピックでは、Windows 8 の PortCls レジストリの電源設定について説明します。
ms.assetid: 148D044E-B736-4526-BDC5-2C180A590C21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e17fd64b7e2ff977bb5b2a470e919eefd7c8b4dd
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035718"
---
# <a name="portcls-registry-power-settings"></a>PortCls レジストリの電源設定


このトピックでは、Windows 8 の PortCls レジストリの電源設定について説明します。

Windows 8 では、(PortCls) ミニポートドライバーは、ドライバーのレジストリキーのレジストリ値を使用して、次の操作を実行できます。

- PortCls がアイドル電源管理を有効にするかどうかを判断する

- バッテリ節約モード (高パフォーマンスモードと比較) のアイドルタイムアウト値を決定する

既定では、PortCls が電源設定を使用して、"デバイスのアイドル" 検出を電源マネージャーに登録するかどうかを決定するために使用される電源設定があります。これは、ランタイム電源フレームワークによって電力が不要になったことが示されたときです。 電源設定プロファイルの記述に使用されるパラメーターは、次のように定義されています。

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
<th align="left">［データの種類］</th>
<th align="left">既定値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ConservationIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0-秒のタイムアウト。</td>
</tr>
<tr class="even">
<td align="left">IdlePowerState</td>
<td align="left">REG_BINARY</td>
<td align="left">3 (D3)
<p>有効な値は:</p>
1-D1 2-D2 3-D3</td>
<td align="left">電力が不要になったときにデバイスが入力する電源の状態を指定します。</td>
</tr>
<tr class="odd">
<td align="left">PerformanceIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0-秒のタイムアウト。</td>
</tr>
</tbody>
</table>

 

次の Windows レジストリフラグメントは、電源設定情報を提供するために使用される構文を示しています。

``` syntax
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4D36E96C-E325-11CE-BFC1-08002BE10318}\0000\PowerSettings]
"ConservationIdleTime"=hex:1e,00,00,00
"PerformanceIdleTime"=hex:00,00,00,00
"IdlePowerState"=hex:03,00,00,00
```

前のフラグメントは、 *ConservationIdleTime*の16進数 (16 進) 値 "1e" を示しています。これは30秒のアイドルタイムアウトに相当します。 *PerformanceIdleTime*に表示される "0" の16進値は、アイドル状態の管理が無効になっていることを意味します。 *IdlePowerState*に表示される "03" の値は、電源が不要になったときに、この電源設定プロファイルに関連付けられているデバイスが D3 電源状態になることを意味します。
