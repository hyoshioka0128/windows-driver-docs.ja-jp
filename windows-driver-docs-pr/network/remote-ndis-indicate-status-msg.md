---
title: REMOTE_NDIS_INDICATE_STATUS_MSG
Description: This message is sent from a Remote NDIS device to a host to indicate a change in the status of the device.
ms.assetid: 768aad13-3da6-436c-a7ba-d420af34643e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26c27b3fb61aacdfc6e9463f47b8041e31a1731f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535485"
---
# <a name="remotendisindicatestatusmsg"></a>リモート\_NDIS\_を示す\_状態\_メッセージ


このメッセージをデバイスの状態の変更を示すために、リモート NDIS デバイスから、ホストに送信されます。 リモート\_NDIS\_を示す\_状態\_メッセージ メッセージが、認識されないメッセージなど、エラー イベントを指定することもできます。 NDIS リモート デバイスでは、リモート NDIS によって初期化された状態になっているとき、このメッセージを送信できます。 このメッセージに応答がありません。

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
<td><p>送信されるメッセージの種類を指定します。 0x00000007 に設定します。</p></td>
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
<td><p>ホストの要求の現在の状態を指定します。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>StatusBufferLength</p></td>
<td><p>状態のデータの長さをバイト単位で指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>StatusBufferOffset</p></td>
<td><p>このメッセージは、デバイスの表示の Rndis_Diagnostic_Info 状態データが存在する場所の先頭からのバイト オフセットを指定します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

リモートの最も一般的な用途\_NDIS\_を示す\_状態\_MSG を 802.3 のデバイスへのリンクの状態を示すことです。 RNDIS のステータス値\_状態\_メディア\_接続することを示しますからの移行には、(たとえばありません 802.3 リンク パルス) が切断されている接続の状態 (802.3 リンクのパルスが検出されました)。 RNDIS のステータス値\_状態\_メディア\_切断は、接続から切断された状態に遷移をことを示します。 デバイスはリモートで送信する必要があります\_NDIS\_を示す\_状態\_MSG これらのいずれかの値を毎回 802.3 リンク状態の変更。 これら 2 つの一般的なことを返すには、バッファーの状態は必要ありません。

ケースでは、デバイスが処理されませんでした、ホストのメッセージへの応答でこのメッセージの送信先、*状態*RNDIS にフィールドを設定する必要があります\_状態\_無効な\_データ、および Rndis\_診断\_情報ステータスのバッファーの形式は次のとおりです。

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
<td><p>DiagStatus</p></td>
<td><p>エラー (たとえば、RNDIS_STATUS_NOT_SUPPORTED) 自体に関するステータス情報が含まれています</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>ErrorOffset</p></td>
<td><p>エラーが検出された元のメッセージでは、0 から始まるバイト オフセットを指定します。</p></td>
</tr>
</tbody>
</table>

 

エラー状態が、リモートの NDIS メッセージによって発生したかどうか (たとえば、認識できないデバイス特定 RNDIS メッセージ)、デバイスは、上記で定義されたステータス メッセージの最後に、元のメッセージを追加する必要があります。

このメッセージは、デバイスが適切な状態で応答メッセージを生成することがない状況でのみ、エラー状態をレポートに使用されます。 適切な使用方法の例は次のとおりです。

-   でサポートされていないメッセージの種類のメッセージを受信します。

-   受信時、 [**リモート\_NDIS\_パケット\_MSG** ](remote-ndis-packet-msg.md)許容できない内容にします。

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

 

 




