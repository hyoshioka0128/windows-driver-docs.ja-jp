---
title: REMOTE_NDIS_SET_MSG
Description: このメッセージは、デバイスにいくつかのオペレーションのパラメーターの値を設定するために必要なときに、ホストからリモートの NDIS デバイスに送信されます。
ms.assetid: d39032e2-e3a5-415f-8bd6-b60b9049ce33
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d730f462919a074f85f869d042480ccace052066
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343184"
---
# <a name="remotendissetmsg"></a>リモート\_NDIS\_設定\_メッセージ


このメッセージは、デバイスにいくつかのオペレーションのパラメーターの値を設定するために必要なときに、ホストからリモートの NDIS デバイスに送信されます。 特定のパラメーターを設定するにを使用してオブジェクト識別子 (OID) は識別され、メッセージと共に送信される情報バッファー内に設定するのには値が含まれています。 ホストをリモート送信\_NDIS\_設定\_デバイスがリモートの NDIS によって初期化された状態である、いつでも制御チャネルを介してそのデバイスへのメッセージ。 リモート NDIS デバイスはリモートを送信することによってこのメッセージに応答\_NDIS\_設定\_CMPLT をホストします。

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
<td><p>送信されるメッセージの種類を指定します。 0x00000005 に設定します。</p></td>
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
<td><p>OID</p></td>
<td><p>設定されているパラメーターを識別する NDIS OID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>要求の入力データの長さをバイト単位で指定します。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>先頭からのバイト オフセットを指定します、 <em>RequestId</em>フィールドに、要求の入力データがあります。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceVcHandle</p></td>
<td><p>接続指向のデバイス用に予約されています。 0 に設定します。</p></td>
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

 

 




