---
title: サポートのレベルを PnP します。
description: サポートのレベルを PnP します。
ms.assetid: 33e0b4c6-858c-4822-ba49-38eb87a5923d
keywords:
- PnP WDK カーネル、デバイスのサポート
- プラグ アンド プレイ WDK カーネル、デバイスのサポート
- 完全な PnP WDK カーネル
- PnP WDK の部分的なカーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1cff716770493462329a32569282fadae54c570
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550935"
---
# <a name="levels-of-support-for-pnp"></a>サポートのレベルを PnP します。





デバイスをサポート PnP エクステントは、デバイスのハードウェアと (次の表を参照してください)、デバイス ドライバーの両方での PnP のサポートに依存します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>PnP ドライバー</th>
<th>非 PnP ドライバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PnP デバイス</strong></p></td>
<td><p>完全な PnP します。</p></td>
<td><p>PnP いいえ</p></td>
</tr>
<tr class="even">
<td><p><strong>非 PnP デバイス</strong></p></td>
<td><p>考えられる部分 PnP</p></td>
<td><p>PnP いいえ</p></td>
</tr>
</tbody>
</table>

 

PnP をサポートする任意のデバイスは、ドライバー、PnP のサポートが必要です。

PnP ドライバーによって決定される場合、非 PnP デバイスは PnP いくつかの機能を持つことができます。 たとえば、ISA のサウンド カード、または EISA ネットワーク カードが手動でインストールされていることができますが、し、PnP ドライバーは PnP デバイスのようにカードを扱うことができます。

ドライバーはサポートしていない PnP、そのデバイスはハードウェア PnP サポートに関係なく、非 PnP デバイスとして動作します。 非 PnP ドライバーでは、システム全体の PnP、電源管理機能を制限できます。

*レガシ ドライバー* (サポートされているオペレーティング システムの前に作成されたドライバー PnP) 以前は、任意の PnP 機能がないと同じ動作を続行します。 新しいドライバーは、PnP サポートを含める必要があります。

 

 




