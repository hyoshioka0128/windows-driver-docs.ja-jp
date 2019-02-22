---
title: REMOTE_NDIS_QUERY_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_QUERY_MSG message with a REMOTE_NDIS_QUERY_CMPLT message.
ms.assetid: 357e2ade-0b67-42c3-b1e1-dcc4b7ec5cda
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 618860ecf39a5660b7a3bc3cf8f4fc9e66b0bf37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553957"
---
# <a name="remotendisquerycmplt"></a>リモート\_NDIS\_クエリ\_CMPLT


リモートの NDIS デバイスが応答する、 [**リモート\_NDIS\_クエリ\_MSG** ](remote-ndis-query-msg.md)でリモート メッセージ\_NDIS\_クエリ\_CMPLT メッセージ。 このメッセージは、ホストにデバイスのパラメーターまたは統計カウンターのクエリの結果を中継に使用されます。 リモートの NDIS デバイスは、このメッセージ内のホストにも、要求された情報を返します。

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
<td><p>送信されるメッセージの種類を指定します。 0x80000004 に設定します。</p></td>
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
<td><p>リモートの NDIS メッセージの ID 値を指定します。 この値は、応答対象 REMOTE_NDIS_QUERY_MSG からコピーされます。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状況</p></td>
<td><p>OID のクエリ要求の処理の状態を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>クエリの応答データの長さをバイト単位で指定します。 OID 結果バッファーが存在しない場合は 0 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>先頭からのバイト オフセットを指定します、 <em>RequestId</em>フィールドに、どの応答クエリのデータが存在する場所。 応答データが存在しない場合は 0 に設定します。</p></td>
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

 

 




