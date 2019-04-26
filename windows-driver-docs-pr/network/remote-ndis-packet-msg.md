---
title: REMOTE_NDIS_PACKET_MSG
Description: REMOTE_NDIS_PACKET_MSG は、1 つのデータのメッセージを形成する NDIS データ パケットをカプセル化します。
ms.assetid: cc4efe94-6e2c-4201-b251-10e76cf5a553
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb6a990e578f3e14634bac684270755004e2afaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350830"
---
# <a name="remotendispacketmsg"></a>リモート\_NDIS\_パケット\_メッセージ


リモート\_NDIS\_パケット\_メッセージは、1 つのデータのメッセージを形成する NDIS データ パケットをカプセル化します。

複数のリモートの連結\_NDIS\_パケット\_フォーム multipacket メッセージのメッセージの要素。 各個々 のリモート\_NDIS\_パケット\_以下に示すように、メッセージのコンポーネントを作成します。 パケットの 1 つのメッセージから異なっているは、 *MessageLength*フィールドには、各リモート\_NDIS\_パケット\_メッセージ ヘッダーには、いくつか追加の埋め込みバイトが含まれます。 最後のリモートがすべてにこれらの埋め込みバイトが追加されます\_NDIS\_パケット\_MSG ように後続リモート\_NDIS\_パケット\_メッセージは、適切なバイト境界で開始します。 各リモート ホストに、デバイスから送信されたメッセージでこの埋め込みが生成\_NDIS\_パケット\_MSG バイトから始まるオフセット multipacket メッセージの先頭から始まる 8 バイトの倍数では。 ホストは、デバイスに multipacket メッセージを送信するときにに従う、 *PacketAlignmentFactor*デバイスを指定します。

リモート\_NDIS\_パケット\_メッセージ形式が次の表で定義されています。

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
<td><p>送信されるメッセージの種類を指定します。 0x1 に設定します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>メッセージの長さ (バイト単位) などには、パケット データ、OOB データ、パケットの情報のデータ、および内部と外部の両方のパディングが追加されます。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>DataOffset</p></td>
<td><p>データの先頭にこのメッセージの DataOffset フィールドの先頭からのバイト オフセットを指定します。 これは、整数値 4 の倍数です。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>DataLength</p></td>
<td><p>このメッセージのデータ コンテンツでは、バイト数を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>OOBDataOffset</p></td>
<td><p>最初の OOB データ レコードの先頭からのバイト オフセットを指定します、 <em>DataOffset</em>このメッセージのフィールド。 OOB のデータが存在しない場合は 0 に設定します。 それ以外の場合、これは、整数値 4 の倍数です。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>OOBDataLength</p></td>
<td><p>OOB のデータの合計の長さ (バイト単位) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>NumOOBDataElements</p></td>
<td><p>このメッセージでは、OOB レコードの数を指定します。</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoOffset</p></td>
<td><p>先頭からのオフセット (バイト単位) を指定します、 <em>DataOffset</em>パケットごとの情報の最初のデータ レコードの先頭に REMOTE_NDIS_PACKET_MSG データ メッセージのフィールド。 パケット単位でデータが存在しない場合は、0 に設定します。 それ以外の場合、これは、整数値 4 の倍数です。</p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoLength</p></td>
<td><p>このメッセージに含まれるパケットごとの情報の合計の長さ (バイト単位) を指定します。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>VcHandle</p></td>
<td><p>接続指向のデバイス用に予約されています。 0 に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>予約済み</p></td>
<td><p>予約済み。 0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

OOB データ レコードを 1 つの形式は次の表に示されます。

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
<td><p>サイズ</p></td>
<td><p>この OOB ヘッダーと追加された OOB データ、および埋め込みのバイト長。 これは、整数値 4 の倍数です。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>種類</p></td>
<td><p>802.3 デバイス用に定義されていません。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>ClassInformationOffset</p></td>
<td><p>OOB データの先頭にこの OOB データ レコードの先頭からのバイト オフセット。</p></td>
</tr>
<tr class="even">
<td><p>(N)</p></td>
<td><p>...</p></td>
<td><p>OOB データ</p></td>
<td><p>OOB データ。詳細については、Microsoft Windows ドライバー開発キット (DDK) ドキュメントを参照してください。</p></td>
</tr>
</tbody>
</table>

 

**注**   (N) はの値と等しい*ClassInformationOffset*します。

 

次の表では、パケットの情報のデータ レコードの形式を定義します。

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
<td><p>サイズ</p></td>
<td><p>このデータ パケット単位でヘッダーとパケット単位で追加されたデータおよび埋め込みのバイト長。 この値は整数 4 の倍数です。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>種類</p></td>
<td><p>Windows 2000 Driver Development Kit (DDK) での説明に従って、NDIS_PER_PACKET_INFO_FROM_PACKET の有効な値のいずれかに設定します。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>PerPacketInformationOffset</p></td>
<td><p>パケットごとの情報のデータの先頭にこのパケットごとの情報のデータ レコードの先頭からのバイト オフセット。</p></td>
</tr>
<tr class="even">
<td><p>(N)</p></td>
<td><p>...</p></td>
<td><p>パケットごとのデータ</p></td>
<td><p>パケットごとのデータ。詳細については、Windows 2000 DDK ドキュメントを参照してください。</p></td>
</tr>
</tbody>
</table>

 

**注**   (N) はの値と等しい*PerPacketInformationOffset*します。

 

<a name="remarks"></a>注釈
-------

各リモート\_NDIS\_パケット\_メッセージは、1 つまたは複数の OOB データ レコードを含めることができます。 *NumOOBDataElements*このメッセージの OOB データ レコードの数を示します。 OOB のデータ レコードは、順番に表示されます必要があります。 *OOBDataLength*フィールド全体の OOB データ ブロックの長さ (バイト単位) を示します。 *OOBDataOffset*フィールドの先頭からのバイト オフセットを示す、 *DataOffset*フィールドを OOB データ ブロックの先頭にします。 OOB のパケット データの詳細については、Windows 2000 DDK の NDIS 仕様を参照してください。

複数の OOB データ ブロックがリモートに関連付けられているかどうかは\_NDIS\_パケット\_メッセージのメッセージを各後続の OOB データ レコードの前の OOB レコードのデータ直後にする必要があります。

802.3 デバイスに現在定義されている OOB 情報はありません。

各リモート\_NDIS\_パケット\_メッセージは、1 つまたは複数のパケット情報データ レコードを含めることができます。 パケット情報は、TCP チェックサムなどのパケットのメタデータを伝達するために使用されます。 *PerPacketInfoOffset*フィールドの先頭からのバイト オフセットを示す、 *DataOffset*パケットごとの情報のデータ レコードの先頭にフィールド。 *OOBDataLength*フィールドをパケット単位で情報のデータ レコードのバイトの長さを示します。 パケットごとの情報のデータの詳細については、Windows 2000 DDK を参照してください。

パケットごとの情報を複数のデータ ブロックがある場合各後続パケットごとの情報のデータ レコードは前のパケットの情報レコードのデータをすぐに従う必要があります。

リモートの NDIS デバイスは、NDIS データ パケットを使用してデータを送受信する必要があります。 デバイスを使用するバスは、ホストに、これらのパケットをホストからデバイスとデバイスに渡される方法を決定します。 共有メモリや、パイプを使用し、USB、アイソクロナス一括の場合です。 アウト オブ バンド (OOB) のデータだけでなく、ネットワーク経由で移動するデータが NDIS パケットに含めることもできます。

リモートの NDIS デバイスとしてカプセル化、NDIS パケットを転送する**リモート\_NDIS\_パケット\_MSG**データ チャネル経由でします。 (802.3) などのコネクションレス型との接続指向の (ATM) などの両方のデバイスでは、同じパケット メッセージ構造を使用して、パケットの処理の一般的なコードを容易にします。 各**リモート\_NDIS\_パケット\_MSG**メッセージには、1 つのネットワーク データ ユニット (s、イーサネット 802.3 フレームなど) に関する情報が含まれています。

帯域外のパケット データまたはデータのパケット情報の詳細については、Windows 2000 DDK NDIS セクションを参照してください。

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

 

 




