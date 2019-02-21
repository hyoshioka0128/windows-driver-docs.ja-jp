---
title: タスクの型を結合する負荷を軽減します。
description: タスクの型を結合する負荷を軽減します。
ms.assetid: 33f8ba3c-09ab-4041-9641-d4207b98c8b7
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、オフロード型を結合します。
- WDK TCP/IP offload タスク オフロードの型を結合します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b387f5092c4abfda70725a7e134df39950d7f978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539134"
---
# <a name="combining-types-of-task-offloads"></a>タスクの型を結合する負荷を軽減します。





次の制限は、NDIS 6.0 とそれ以降のタスク オフロード サービスの組み合わせは、システムでアクティブにできるを決定します。

-   タスクのオフロード対応ミニポート アダプターでは、単独でチェックサム オフロードをサポートできます。

-   大量送信オフロード バージョン 1 (LSOV1)-対応のネットワーク インターフェイス カード (NIC) は、V4 TCP をサポートする必要があり、IPv4 チェックサム送信サービスの負荷を軽減します。 LSOV1 対応のミニポート アダプターには、インターネット プロトコル セキュリティ (IPsec) の負荷を軽減もサポートしています、NDIS は IPsec または LSOV1 のいずれかが負荷を軽減するアダプターを構成します。

-   大量送信オフロード バージョン 2 (LSOV2)-対応ミニポート アダプターで TCP をサポートする必要があり、チェックサムの IP 転送をオフロードします。 NDIS は、LSOV2 対応ミニポート アダプターも IPsec オフロードをサポートすると、IPsec または LSOV2、両方ではなくをオフロードすることが構成されます。

ミニポート ドライバーでは、IPv4 と IPv6 の両方をサポートする必要はありません。 すべての NDIS 6.0 とそれ以降のミニポート ドライバーは、イーサネット 802.1 q タグをサポートすることができます、イーサネット 802.3 をカプセル化をサポートする必要があります。 次の表では、ミニポート ドライバーはさまざまなオフロード機能のサポートを報告したときにハードウェア要件について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オフロードの種類</th>
<th align="left">IPv4</th>
<th align="left">IpV6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>チェックサム オフロード</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>UDP チェックサム</p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>省略可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TCP チェックサム</p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>省略可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>TCP オプション</p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>(TCP チェックサム) に必要な</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP チェックサム</p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>適用不可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP オプション</p></td>
<td align="left"><p>(TCP チェックサム) に必要な</p></td>
<td align="left"><p>適用不可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拡張機能の IP ヘッダー</p></td>
<td align="left"><p>適用不可能</p></td>
<td align="left"><p>必要な (128 バイト)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大規模なオフロード送信のバージョン 1 (LSOv1)</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>オフロードの最大サイズ</p></td>
<td align="left"><p>&lt;= 64 K</p></td>
<td align="left"><p>適用不可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>TCP オプション</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>適用不可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP オプション</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>適用不可能</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大規模な Send Offload バージョン 2 (LSOv2)</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>オフロードの最大サイズ</p></td>
<td align="left"><p>無制限</p></td>
<td align="left"><p>無制限</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP オプション</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>必要な (128 バイト)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP ID のサポート</p></td>
<td align="left"><p>0 xffff を 0x0000</p></td>
<td align="left"><p>0x0000 に 0x7fff セグメント化用に予約された負荷を軽減します。</p></td>
</tr>
</tbody>
</table>

 

 

 





