---
title: REMOTE_NDIS_RESET_MSG
Description: このメッセージは、ホストからデバイスをリセットし、リターン ステータスに NDIS リモート デバイスに送信されます。
ms.assetid: b5938b0d-75bf-497f-afeb-9950b383af5e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: beed2ca885a5d76af4f43c1efc58411b215e3bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351260"
---
# <a name="remotendisresetmsg"></a>リモート\_NDIS\_リセット\_メッセージ


このメッセージは、ホストからデバイスをリセットし、リターン ステータスに NDIS リモート デバイスに送信されます。 ホストをリモート送信\_NDIS\_リセット\_デバイスがリモートの NDIS によって初期化された状態である、いつでも制御チャネルを介してそのデバイスへのメッセージ。 リモート NDIS デバイスはリモートを送信することによってこのメッセージに応答\_NDIS\_リセット\_CMPLT をホストします。

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
<td><p>送信されるメッセージの種類を指定します。 0x00000006 に設定します。</p></td>
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
<td><p>予約済み</p></td>
<td><p>予約済み。 0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

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

 

 




