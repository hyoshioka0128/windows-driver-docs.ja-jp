---
title: REMOTE_NDIS_RESET_CMPLT
Description: リモートの NDIS デバイスは、デバイスをリセットし、REMOTE_NDIS_RESET_CMPLT メッセージ要求の状態を返すことで、ホストから REMOTE_NDIS_RESET_MSG メッセージに応答します。
ms.assetid: 80ab998f-9690-49d3-bb47-1937c832d13e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853e8d4fc849662eeda2426c504b50e570b238c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388124"
---
# <a name="remotendisresetcmplt"></a>リモート\_NDIS\_リセット\_CMPLT


リモートの NDIS デバイスが応答する、 [**リモート\_NDIS\_リセット\_MSG** ](remote-ndis-reset-msg.md)デバイスをリセットし、要求の状態を返すことで、ホストからのメッセージリモートの\_NDIS\_リセット\_CMPLT メッセージ。

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
<td><p>送信されるメッセージの種類を指定します。 0x80000006 に設定します。</p></td>
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
<td><p>状況</p></td>
<td><p>リセット要求を処理の状態を指定します。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>AddressingReset</p></td>
<td><p>かどうか、アドレス情報 (マルチキャスト アドレスの一覧、パケット フィルター) が失われたあるいはのリセット操作中を示します。 デバイスが再送信するホストが必要な場合に表示されますこのフィールドを設定するアドレス指定情報を。それ以外の場合 0 に設定します。</p></td>
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

 

 




