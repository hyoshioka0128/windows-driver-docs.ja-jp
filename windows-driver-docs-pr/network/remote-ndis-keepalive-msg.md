---
title: REMOTE_NDIS_KEEPALIVE_MSG
Description: ホストは、定期的に行われていないその他のコントロールやデータからのトラフィック デバイス bus によって定義された KeepAliveTimeoutPeriod をホストするときに、このメッセージを送信します。
ms.assetid: 7e0b329f-8ba7-488d-b99d-63e6b9bbc171
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f9415e36ec305b1fb0df2e30106d8f4398d051f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350855"
---
# <a name="remotendiskeepalivemsg"></a>リモート\_NDIS\_KEEPALIVE\_メッセージ


ホストが行われていないその他のコントロールまたはデータ トラフィック、デバイスから bus によって定義されたホストに、定期的に、このメッセージを送信*KeepAliveTimeoutPeriod*します。 このメッセージは、少なくとも RNDIS ホストによって送信\_KEEPALIVE\_タイムアウト (秒)、その他のメッセージ トラフィックがない場合にリモート デバイスの状態を検出します。 リモート デバイスは逆の方向で、同じメッセージを使用する可能性がありますが、必須ではありません。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>サイズ</th>
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>[MessageType]</p></td>
<td><p>送信されるメッセージの種類を指定します。 0x00000008 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>メッセージの先頭からこのメッセージの合計の長さ (バイト単位) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>リモートの NDIS メッセージの ID 値を指定します。 この値は、デバイスの応答を持つホストによって送信されたメッセージに一致するように使用されます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ホストは、リモートを送信しません\_NDIS\_KEEPALIVE\_RNDIS までメッセージのメッセージ\_KEEPALIVE\_タイムアウト (秒) は、リモート デバイスから受信した最後のメッセージから経過しました。 これにより、通信チャネルがアクティブのとき、キープ アライブ メッセージの不要な exchange を回避できます。

デバイスは、ホストもこのメッセージを送信することができます必要に応じて。 たとえば、デバイスでは、ラウンド トリップ遅延時間を計算するため、ホストからの応答をトリガーするのにこのメッセージを使用する可能性があります。 実装されている場合、デバイスがリモートを送信する必要があります\_NDIS\_KEEPALIVE\_MSG コントロール チャネルと、デバイスがリモートの NDIS によって初期化された状態が場合にのみ使用します。

ホストの送信、**リモート\_NDIS\_KEEPALIVE\_MSG**コントロール チャネルを介してデバイスにメッセージをデバイスの正常性を確認します。 ホストが行われていないその他のコントロールまたはデータ トラフィック、デバイスからのホストに、定期的にこのメッセージを送信リモート NDIS によって初期化された状態で、デバイスがある場合、 *KeepAliveTimeoutPeriod*します。 *KeepAliveTimeoutPeriod*バスに依存し、適切な bus マッピング仕様で定義されます。

このメッセージを受信すると、リモート デバイスが応答を返す必要がありますが*状態*フィールドは、デバイスを活用しているかどうかを示す、 [**リモート\_NDIS\_リセット\_MSG** ](remote-ndis-reset-msg.md)ホストからのメッセージ。

デバイスは、表示が停止した場合に、特定のアクションを実行する必要はありません**リモート\_NDIS\_KEEPALIVE\_MSG**ホストからのメッセージ。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。 としても使用可能では、Windows 2000 バイナリの再頒布可能パッケージ。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Rndis.h (Rndis.h を含む)</td>
</tr>
</tbody>
</table>

 

 




