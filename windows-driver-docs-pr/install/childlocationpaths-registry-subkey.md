---
title: ChildLocationPaths レジストリのサブキー
description: ChildLocationPaths レジストリのサブキー
ms.assetid: 9c485981-e9f8-420d-9a87-d298b55356c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b1df40309d1743642e0f27b87d0871e992b7a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537235"
---
# <a name="childlocationpaths-registry-subkey"></a>ChildLocationPaths レジストリのサブキー


以降、Windows 7 では、 **ChildLocationPaths** HardwareID のいずれかで識別されるデバイスのレジストリ サブキーがリムーバブル デバイス機能のオーバーライドの指定で使用される) は、リムーバブル デバイスありません適用される機能をオーバーライドします。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

**ChildLocationPaths**レジストリ サブキーが親の名前で指定されたデバイスの子 devnode のみに適用されます**HardwareID**または**CompatibleID**サブキー。 結果として、リムーバブル デバイスの機能の上書き値によって、指定されたデバイスの子 devnode のみが影響を受けます。 指定したデバイスの親 devnode の影響を受けない、リムーバブル デバイス機能上書きしない限り、 [ **LocationPaths** ](locationpaths-registry-subkey.md)レジストリ サブキーが指定されても、 **ChildLocationPaths**親 devnode のレジストリ サブキーが指定されています。

次の表形式およびの要件の定義、 **ChildLocationPaths**レジストリ サブキー。

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
<th align="left">親のサブキー</th>
<th align="left">子のサブキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ChildLocationPaths</strong></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>または<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a>または <a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
</tr>
</tbody>
</table>

 

**注**  か、 [ **LocationPaths** ](locationpaths-registry-subkey.md)または**ChildLocationPaths**レジストリ サブキーを親/子を示すために存在する必要がありますリムーバブル デバイスの機能をオーバーライドするリレーションシップが適用されます。

 

 

 





