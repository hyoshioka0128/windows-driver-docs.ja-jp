---
title: REMOTE_NDIS_SET_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_SET_MSG message with a REMOTE_NDIS_SET_CMPLT message.
ms.assetid: 97436a5f-7516-46cf-b789-a6b1c8c067a2
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3664bd100a640d6ece3441b68a3f1242c60e595
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580283"
---
# <a name="remotendissetcmplt"></a>リモート\_NDIS\_設定\_CMPLT


リモートの NDIS デバイスが応答する、 [**リモート\_NDIS\_設定\_MSG** ](remote-ndis-set-msg.md)でリモート メッセージ\_NDIS\_セット\_CMPLT メッセージ。 このメッセージは、ホストへのデバイスの操作パラメーターの値の設定の結果を中継に使用されます。

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
<td><p>送信されるメッセージの種類を指定します。 0x80000005 に設定します。</p></td>
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
<td><p>リモートの NDIS メッセージの ID 値を指定します。 この値は、応答対象 REMOTE_NDIS_SET_MSG からコピーされます。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状態</p></td>
<td><p>OID のセット要求を処理の状態を指定します。</p></td>
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

 

 




