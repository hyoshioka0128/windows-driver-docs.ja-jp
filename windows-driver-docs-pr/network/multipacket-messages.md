---
title: マルチパケット メッセージ
description: マルチパケット メッセージ
ms.assetid: 58979799-4618-43b9-a6dc-0635f6ade9b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b441642ac3f61e53e156e504c9c06178bb380419
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393085"
---
# <a name="multipacket-messages"></a>マルチパケット メッセージ





複数[**リモート\_NDIS\_パケット\_MSG** ](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))いずれかの方向の 1 つの転送にメッセージを送信できます。 Multipacket メッセージが複数の連結して形成された**リモート\_NDIS\_パケット\_MSG**要素。 このような転送の最大長に準拠するもの、 *MaxTransferSize*パラメーターが渡された、 [**リモート\_NDIS\_初期化\_MSG**](https://docs.microsoft.com/previous-versions/ff570624(v=vs.85))と応答メッセージ。 ホストがメッセージへの転送を 1 つに、バンドルの数を制限しても、 *MaxPacketsPerMessage*にデバイスによって返されるパラメーター、 [**リモート\_NDIS\_初期化\_CMPLT** ](https://docs.microsoft.com/previous-versions/ff570621(v=vs.85))応答メッセージ。

メッセージの単一パケットの場合はその違いは、 *MessageLength*フィールドでそれぞれ[**リモート\_NDIS\_パケット\_MSG** ](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))ヘッダーには、いくつか追加の埋め込みバイトが含まれます。 すべては、最後にこれらの埋め込みバイトが追加**リモート\_NDIS\_パケット\_MSG**ように後続リモート\_NDIS\_パケット\_メッセージ適切なバイトの境界から開始します。 各リモート ホストに、デバイスから送信されたメッセージでこの埋め込みが生成\_NDIS\_パケット\_MSG バイトから始まるオフセット multipacket メッセージの先頭から始まる 8 バイトの倍数では。 ホストは、デバイスに multipacket メッセージを送信するときにに従う、 *PacketAlignmentFactor*内のデバイスで指定された、 [**リモート\_NDIS\_INITIALIZE\_CMPLT** ](https://docs.microsoft.com/previous-versions/ff570621(v=vs.85))応答メッセージ。

なお multipacket メッセージの数のどちらを合わせた長さ[**リモート\_NDIS\_パケット\_MSG** ](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))まとめられたメッセージ内の要素が与えられます明示的に、リモートの NDIS フィールドを定義します。 合わせた長さは、バスに固有の転送メカニズムで暗黙的で、ホストまたはデバイスが説明する必要があります、 *MessageLength*の数を決定する結合のメッセージのフィールドは、メッセージを結合します。

次の表に、2 つのリモートで構成される multipacket メッセージの例は、\_NDIS\_パケット\_ホストからデバイスへ送信されるメッセージ。 中に、 [**リモート\_NDIS\_初期化\_MSG** ](https://docs.microsoft.com/previous-versions/ff570624(v=vs.85))交換については、要求されたデバイス、 *PacketAlignmentFactor* (3配置を 8 バイト境界に沿って)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">サイズ</th>
<th align="left">フィールド</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>[MessageType]</p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageLength</p></td>
<td align="left"><p>72 (2 つの埋め込みバイトが含まれています以下をご覧ください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataOffset</p></td>
<td align="left"><p>36</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataLength</p></td>
<td align="left"><p>26</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>24</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>NumOOBDataElements</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>VcHandle</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>26</p></td>
<td align="left"><p>ペイロード (データ)</p></td>
<td align="left"><p>いくつかのネットワーク 26 バイト長のデータ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>余白</p></td>
<td align="left"><p>問題ではありません - 未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>72</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageType (2 つ目の開始<a href="https://docs.microsoft.com/previous-versions/ff570635(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))"> <strong>REMOTE_NDIS_PACKET_MSG</strong></a>)</p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>76</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageLength</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>80</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataOffset</p></td>
<td align="left"><p>36</p></td>
</tr>
<tr class="odd">
<td align="left"><p>84</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataLength</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>88</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>92</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>96</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>NumOOBDataElements</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>100</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>104</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>108</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>VcHandle</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>112</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>116</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>ペイロード (データ)</p></td>
<td align="left"><p>一部のネットワーク データの長さは 16 バイト</p></td>
</tr>
</tbody>
</table>

 

 

 





