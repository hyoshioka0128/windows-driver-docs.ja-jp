---
title: LocationPaths レジストリのサブキー
description: LocationPaths レジストリのサブキー
ms.assetid: d34ba7f4-97d2-4e63-a820-436c0336c584
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62970aff742d93ad3f4410ace59a506726a84a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532562"
---
# <a name="locationpaths-registry-subkey"></a>LocationPaths レジストリのサブキー


Windows 7 以降、 **LocationPaths** HardwareID のいずれかで識別されるデバイスのレジストリ サブキーがリムーバブル デバイス機能のオーバーライドの指定で使用される) リムーバブル デバイスの機能が提供されます上書きを適用します。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

**LocationPaths**レジストリ サブキーは、デバイスの名前を使用して指定の親 devnode のみに適用されます、 **HardwareID**または**CompatibleID**サブキー。 その結果、リムーバブル デバイスの機能の上書き値を指定されたデバイスの親 devnode のみが影響を受けます。 指定したデバイスの子 devnode の影響を受けない、リムーバブル デバイス機能の上書きしない限り、 [ChildLocationPaths](childlocationpaths-registry-subkey.md)レジストリ サブキーが指定されてもします。

次の表形式およびの要件の定義、 **LocationPaths**レジストリ サブキー。

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
<td align="left"><p><strong>LocationPaths</strong></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>または<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a>または <a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
</tr>
</tbody>
</table>

 

いずれか、 **LocationPaths**または[ChildLocationPaths](childlocationpaths-registry-subkey.md)レジストリ サブキーをリムーバブル デバイスの機能をオーバーライドする親/子リレーションシップが適用対象を示すために存在する必要があります。

 

 





