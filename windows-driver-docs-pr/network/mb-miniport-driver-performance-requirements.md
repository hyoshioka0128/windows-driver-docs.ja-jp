---
title: MB ミニポート ドライバーのパフォーマンス要件
description: MB ミニポート ドライバーのパフォーマンス要件
ms.assetid: 16986208-7572-412d-8839-71f1a66b074f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ebb0720bed88b7add196dc84f88210bf2bf727
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844283"
---
# <a name="mb-miniport-driver-performance-requirements"></a>MB ミニポート ドライバーのパフォーマンス要件


次の表では、MB のミニポートドライバーが異なる MB 操作に応答することを想定しています。 最良の結果を得るために、ミニポートドライバーは、"Best case time (sec)" 列で特定された時間内に操作を完了する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MB 操作</th>
<th align="left">最適なケース時間 (秒)</th>
<th align="left">最悪の場合の時間 (秒)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>コンピューターへの挿入後にデバイスが ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state" data-raw-source="[&lt;strong&gt;WwanReadyStateInitialized&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state)"><strong>WwanReadyStateInitialized</strong></a>に到着するまで) 初期化する時間 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info" data-raw-source="[OID_WWAN_READY_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)">OID_WWAN_READY_INFO</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>手動によるネットワーク登録 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state" data-raw-source="[OID_WWAN_REGISTER_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)">OID_WWAN_REGISTER_STATE</a>)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>50</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワークスキャン操作 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers" data-raw-source="[OID_WWAN_VISIBLE_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)">OID_WWAN_VISIBLE_PROVIDERS</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>200</p></td>
</tr>
<tr class="even">
<td align="left"><p>パケットアタッチ操作 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service" data-raw-source="[OID_WWAN_PACKET_SERVICE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)">OID_WWAN_PACKET_SERVICE</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>パケット切断操作 (OID_WWAN_PACKET_SERVICE)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDP のライセンス認証 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect" data-raw-source="[OID_WWAN_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)">OID_WWAN_CONNECT</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PDP の非アクティブ化 (OID_WWAN_CONNECT)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP アドレス、デフォルトゲートウェイ、および DNS アドレスを使用してシステムを更新する</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PDP のアクティブ化後の<a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)"><strong>NDIS_STATUS_LINK_STATE</strong></a>通知</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>次の PIN 操作の完了 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin" data-raw-source="[OID_WWAN_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)">OID_WWAN_PIN</a>):</p>
<p>Enter</p>
<p>[有効にする]</p>
<p>[無効にする]</p>
<p>[Change]</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クエリ OID_WWAN_PIN を実行して、MB デバイスの現在の PIN の状態を取得します。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている PIN の種類の一覧を取得するための<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list" data-raw-source="[OID_WWAN_PIN_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)">OID_WWAN_PIN_LIST</a> response</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SMS サブシステムの準備が完了するまでの時間 (NDIS_STATUS_WWAN_SMS_CONFIGURATION の要請なしの通知を送信する必要があります)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>この表に記載されていない OID_WWAN_VENDOR_SPECIFIC を除く、ミニポートドライバーが他のすべての WWAN Oid を完了するまでの時間</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

 

 





