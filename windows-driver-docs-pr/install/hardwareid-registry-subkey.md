---
title: HardwareID レジストリ サブキー
description: HardwareID レジストリ サブキー
ms.assetid: c6c52aa1-68ee-4d64-be97-509203db6970
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b12f89fb71ef18c2cdeadd3e03caacc67d84f4f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348647"
---
# <a name="hardwareid-registry-subkey"></a>HardwareID レジストリ サブキー


Windows 7 以降、 **HardwareID**レジストリ サブキーでは、リムーバブル デバイスの機能をコンピューターにインストールされているデバイスのオーバーライドを指定します。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

名前、 **HardwareID**レジストリ サブキーを指定します、[ハードウェア ID](hardware-ids.md)デバイスは以下の要件に基づいて書式設定するとします。

次の表形式およびの要件の定義、 **HardwareID**レジストリ サブキー。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ サブキーの名前</th>
<th align="left">必須/省略可能</th>
<th align="left">形式の要件</th>
<th align="left">親キー</th>
<th align="left">子のサブキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>有効な<a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">ハードウェア ID</a>値</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>ハードウェアを含める必要があります bus プレフィックスの ID。</p>
<p>すべてはスラッシュ () のパス区切り記号 (#) 文字の数値 ID を置き換える必要があるハードウェア内です。</p></td>
<td align="left"><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

ハードウェア ID の値は、次の表で説明されている形式の要件に従う必要があります。 各**HardwareID**サブキーは、いずれかを指定する必要があります、 **LocationPaths**または**ChildLocationPaths**サブキー。 内で両方のサブキーが指定されて、 **HardwareID**サブキーを必要な場合。

スラッシュ文字が有効なレジストリ サブキーの名前の文字ではないため、する必要があります文字で置き換えて、番号のバスのプレフィックスを指定するときに、 **HardwareID**レジストリ サブキーの名前。 [デバイス] ノードの場合は、リムーバブル デバイスの機能をオーバーライドを指定するなど、(*devnode*) で、[ハードウェア ID](hardware-ids.md) USB の\\VID_1234 & PID_ABCD & REV_0001、作成する必要が、**HardwareID** USB の名前のレジストリ サブキー\#VID_1234 & PID_ABCD REV_0001 します。

 

 





