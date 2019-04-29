---
title: REMOTE_NDIS_QUERY_MSG
Description: このメッセージは、その特性、統計情報、または状態のデバイスを照会する必要があるとき、ホストからリモート NDIS デバイスに送信されます。
ms.assetid: 9cf79495-a115-49ce-a0cf-fa4fa2183a8a
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c8e89f517f7992b2c4ca9c28835678531ec018e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385484"
---
# <a name="remotendisquerymsg"></a>リモート\_NDIS\_クエリ\_メッセージ


このメッセージは、その特性、統計情報、または状態のデバイスを照会する必要があるとき、ホストからリモート NDIS デバイスに送信されます。 照会するパラメーターまたは統計カウンターは、NDIS オブジェクト識別子 (OID) を使用して識別されます。 ホストをリモート送信\_NDIS\_クエリ\_デバイスがリモートの NDIS によって初期化された状態である、いつでも制御チャネルを介してそのデバイスへのメッセージ。 リモート NDIS デバイスはリモートを送信することによってこのメッセージに応答\_NDIS\_クエリ\_CMPLT をホストします。

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
<td><p>送信されるメッセージの種類を指定します。 0x00000004 に設定します。</p></td>
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
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>OID</p></td>
<td><p>クエリ対象のパラメーターを識別する NDIS OID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>クエリの入力データの長さ (バイト単位) を指定します。 OID 入力バッファーが存在しない場合は 0 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>先頭からのバイト オフセットを指定します、 <em>RequestId</em>フィールド、クエリの入力データがあります。 OID 入力バッファーが存在しない場合は 0 に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceVcHandle</p></td>
<td><p>接続指向のデバイス用に予約されています。 0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

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

 

 




