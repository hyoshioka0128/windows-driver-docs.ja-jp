---
title: Hyper-V 拡張可能スイッチの送信および受信操作
description: Hyper-V 拡張可能スイッチの送信および受信操作
ms.assetid: 3BC59344-CF8E-436F-A1C9-883707990C7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d470df5e2414a6a20c3a73e6de954f0a4eb49bd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574770"
---
# <a name="hyper-v-extensible-switch-send-and-receive-operations"></a>Hyper-V 拡張可能スイッチの送信および受信操作


このセクションでは、送信をについて説明し、HYPER-V 拡張可能スイッチの拡張機能の操作を受信します。 次の表では、拡張機能が拡張可能スイッチのデータ パス経由で送受信パケットで実行できる操作について説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left"><a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">キャプチャ拡張機能</a></th>
<th align="left"><a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">フィルター拡張機能</a></th>
<th align="left"><a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">転送拡張機能</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">元のパケット</td>
<td align="left">x</td>
<td align="left">X</td>
<td align="left">x</td>
</tr>
<tr class="even">
<td align="left">パケットの複製</td>
<td align="left"></td>
<td align="left">x</td>
<td align="left">x</td>
</tr>
<tr class="odd">
<td align="left">パケットを転送</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">x</td>
</tr>
</tbody>
</table>

 

ここでは、次のトピックについて説明します。

[元のパケット トラフィック](originating-packet-traffic.md)

[トラフィックのパケットの複製](cloning-or-duplicating-packet-traffic.md)

[HYPER-V 拡張可能なスイッチ ポートにパケットを転送](forwarding-packets-to-hyper-v-extensible-switch-ports.md)

拡張可能スイッチのデータ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)します。

 

 





