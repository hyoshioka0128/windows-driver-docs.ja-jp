---
title: CompatibleID レジストリ サブキー
description: CompatibleID レジストリ サブキー
ms.assetid: 0111b013-d559-47bb-9cc8-d3930661a0a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfb020c44d30f13303b8df5c7206c688ae519ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361157"
---
# <a name="compatibleid-registry-subkey"></a>CompatibleID レジストリ サブキー


Windows 7 以降、 **CompatibleID**レジストリ サブキーでは、リムーバブル デバイスの機能をコンピューターにインストールされているデバイスのオーバーライドを指定します。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

名前、 **CompatibleID**レジストリ サブキーを指定します、[互換性 ID](compatible-ids.md)デバイスは以下の要件に基づいて書式設定するとします。

次の表形式およびの要件の定義、 **CompatibleID**レジストリ サブキー。

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
<td align="left"><p>有効な<a href="compatible-ids.md" data-raw-source="[compatible ID](compatible-ids.md)">互換性 ID</a>値</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>この互換性のあるを含める必要があります bus プレフィックスの ID。</p>
<p>数 (#) 文字では、すべてスラッシュ () のパスの区切り記号内での互換性のある ID を置き換える必要があります。</p></td>
<td align="left"><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>や<a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
</tr>
</tbody>
</table>

 

互換性のある ID 値は、次の表で説明されている形式の要件に従う必要があります。 各**CompatibleID**サブキーは、いずれかを指定する必要があります、 **LocationPaths**または**ChildLocationPaths**サブキー。 内で両方のサブキーが指定されて、 **CompatbleID**サブキーを必要な場合。

スラッシュ文字が有効なレジストリ サブキーの名前の文字ではないため、する必要があります文字で置き換えて、番号のバスのプレフィックスを指定するときに、 **CompatibleID**レジストリ サブキーの名前。 [デバイス] ノードの場合は、リムーバブル デバイスの機能をオーバーライドを指定するなど、(*devnode*) で、[ハードウェア ID](hardware-ids.md) pci\\VEN_ABCD & DEV_1234 & SUBSYS_000、作成する必要が、**CompatibleID** PCI の名前のレジストリ サブキー\#VEN_ABCD & DEV_1234 SUBSYS_000 します。

 

 





