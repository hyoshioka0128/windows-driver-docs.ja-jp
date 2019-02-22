---
title: REMOTE_NDIS_HALT_MSG
Description: This message is sent by the host to terminate the network connection.
ms.assetid: ad7802ff-20ee-4228-b236-a2ca39e8c478
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c12ac1133475961bc85d0431338698187dc39cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531343"
---
# <a name="remotendishaltmsg"></a>リモート\_NDIS\_HALT\_メッセージ


このメッセージは、ネットワーク接続を終了する、ホストによって送信されます。 その他のコントロールのホスト側開始のメッセージとは異なりは、デバイスはリモートに応答しない\_NDIS\_HALT\_メッセージ。

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
<td><p>メッセージの種類</p></td>
<td><p>送信されるメッセージの種類を指定します。 0x00000003 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>メッセージの先頭からのこのメッセージの合計の長さ (バイト単位) を指定します。</p></td>
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

リモートを実装するためにデバイスを省略できます\_NDIS\_HALT\_メッセージ。 実装されている場合、デバイスは、デバイスがリモートの NDIS によって初期化された状態の場合にのみ、コントロール チャネルを介してホストをこのメッセージを送信します。 デバイスは、このメッセージの送信後すぐにすべての通信を終了する必要があります。 このメッセージを送信することにより、デバイスでリモート NDIS 初期化されない状態を入力します。

このメッセージの受信には、すべての未処理の要求とパケットを破棄する必要があります。

<a name="requirements"></a>要件
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

 

 




