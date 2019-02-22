---
title: クラスの通信インターフェイス
description: クラスの通信インターフェイス
ms.assetid: b0414d0e-6e1b-4d84-8ca4-40a59fb1b099
keywords:
- 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be9190ea105d99730974e2ad6140e5f96bad71a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556944"
---
# <a name="communication-class-interface"></a>クラスの通信インターフェイス





クラスの通信インターフェイスは、USB インターフェイスの記述子を次の 3 つのクラスに固有の記述子、および通知エンドポイントのエンドポイント記述子によって記述されます。 通知のエンドポイント記述子は、標準的な USB 中断タイプのエンドポイント記述子が**wMaxPacketSize**フィールドは 8 バイトです。 次の表では、通信クラス インターフェイスの記述子の著名なフィールドを定義します。

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
<th align="left">オフセット (バイト)</th>
<th align="left">フィールド</th>
<th align="left">サイズ (バイト)</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
<td align="left"><p>通信インターフェイス クラスのコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
<td align="left"><p>コントロールの抽象モデルの通信インターフェイス クラスのサブクラス コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>FFh</p></td>
<td align="left"><p>ベンダーの特定のプロトコルの通信インターフェイス クラス プロトコルのコードです。</p></td>
</tr>
</tbody>
</table>

 

 

 





