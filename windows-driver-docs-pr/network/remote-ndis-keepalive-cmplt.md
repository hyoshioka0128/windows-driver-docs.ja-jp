---
title: REMOTE_NDIS_KEEPALIVE_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_KEEPALIVE_MSG message from the host by sending back a REMOTE_NDIS_KEEPALIVE_CMPLT response message.
ms.assetid: c090b781-73f1-4a7a-a0a2-60af366daa77
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69abf349b66b4307f62d00827d79829660822ae8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531413"
---
# <a name="remotendiskeepalivecmplt"></a>リモート\_NDIS\_KEEPALIVE\_CMPLT


リモートの NDIS デバイスが応答する、 [**リモート\_NDIS\_KEEPALIVE\_MSG** ](remote-ndis-keepalive-msg.md)返送してリモートでホストからのメッセージ\_NDIS\_KEEPALIVE\_CMPLT 応答メッセージ。 返された状態でない RNDIS 場合\_状態\_成功すると、ホストは送信[**リモート\_NDIS\_リセット\_MSG** ](remote-ndis-reset-msg.md)をリセットする、デバイスです。

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
<td><p>送信されるメッセージの種類を指定します。 0x80000008 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>メッセージの先頭からこのメッセージの合計の長さをバイト単位で指定します。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>リモートの NDIS メッセージの ID 値を指定します。 この値は、デバイスの応答を持つホストによって送信されたメッセージに一致するように使用されます。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状況</p></td>
<td><p>デバイスの現在の状態を指定します。 場合、返された<em>状態</em>ない RNDIS_STATUS_SUCCESS、ホストは送信、 <a href="remote-ndis-reset-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_RESET_MSG&lt;/strong&gt;](remote-ndis-reset-msg.md)"> <strong>REMOTE_NDIS_RESET_MSG</strong> </a>メッセージ、デバイスをリセットします。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバイスに送信するオプションが実装されている場合[**リモート\_NDIS\_KEEPALIVE\_MSG**](remote-ndis-keepalive-msg.md)、リモート ホストは応答を\_NDIS\_KEEPALIVE\_コントロール チャネルを介して CMPLT します。

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

 

 




