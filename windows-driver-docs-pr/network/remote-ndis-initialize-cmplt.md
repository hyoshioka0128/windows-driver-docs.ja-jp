---
title: REMOTE_NDIS_INITIALIZE_CMPLT
ms.assetid: e1e057bf-aa92-4b90-b993-a82cc260ff7f
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 599c811c124304595867c899fd750bdaa15dd45c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350887"
---
# <a name="remotendisinitializecmplt"></a>リモート\_NDIS\_初期化\_CMPLT


リモート\_NDIS\_初期化\_への応答で、ホスト、リモートの NDIS デバイスから送信される CMPLT メッセージ、 [**リモート\_NDIS\_初期化\_MSG** ](remote-ndis-initialize-msg.md)メッセージ。 リモートの\_NDIS\_初期化\_CMPLT メッセージ、デバイスのメディアの種類、リモートの NDIS バージョン番号、およびその型のレポート (または接続指向のコネクションレス型またはその両方)。

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
<td><p>送信されるメッセージの種類を指定します。 0x80000002 に設定します。</p></td>
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
<td><p>状況</p></td>
<td><p>RNDIS_STATUS_SUCCESS を指定しますデバイスが正常に初期化されている場合。それ以外の場合、エラーを示すエラー コードを指定します。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>MajorVersion</p></td>
<td><p>デバイスでサポートされている最も高いリモート NDIS 主要なプロトコルのバージョンを指定します。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>デバイスでサポートされている最も高いリモート NDIS マイナー プロトコルのバージョンを指定します。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceFlags</p></td>
<td><p>コネクションレス型または接続指向のいずれかとして、ミニポート ドライバーの種類を指定します。 この値には、次のいずれかを指定できます。</p>
<p>RNDIS_DF_CONNECTIONLESS 0x00000001</p>
<p>RNDIS_DF_CONNECTION_ORIENTED 0x00000002</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>中</p></td>
<td><p>デバイスでサポートされているメディアを指定します。 RNDIS_MEDIUM_802_3 に設定 (0x00000000)</p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>MaxPacketsPerMessage</p></td>
<td><p>1 つの転送では、デバイスが処理できるリモート NDIS データ メッセージの最大数を指定します。 この値は、少なくとも 1 つである必要があります。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>デバイスが、ホストから受信する 1 つのバス データ転送はすべてのバイト単位の最大サイズを指定します。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>PacketAlignmentFactor</p></td>
<td><p>デバイスが期待する multimessage の転送に含まれている各リモート NDIS メッセージ バイトのアラインメントを指定します。 この値は、2 の累乗で指定されます。 たとえば、この値は 8 バイト アラインメントを示すを 3 つ設定します。 この値には、最大 7 128 バイトのアラインメントを指定する設定があります。</p></td>
</tr>
<tr class="even">
<td><p>44</p></td>
<td><p>4</p></td>
<td><p>AFListOffset</p></td>
<td><p>接続指向のデバイス用に予約されています。 値を 0 に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>48</p></td>
<td><p>4</p></td>
<td><p>AFListSize</p></td>
<td><p>接続指向のデバイス用に予約されています。 値を 0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*状態*RNDIS にフィールドを設定する必要があります\_状態\_正常。 それ以外の場合、デバイスが初期化されている場合は、成功、失敗を示すエラー コードに設定されます。 デバイスで、サポートできる最も高いリモート NDIS プロトコルのバージョンを返す必要があります*MajorVersion*と*MinorVersion*--組み合わせたバージョン番号は、バージョン番号未満にする必要があります指定されたホスト、 [**リモート\_NDIS\_初期化\_MSG** ](remote-ndis-initialize-msg.md)メッセージ。

*AFListSize*と*AFListOffset*フィールドは、コール マネージャーを含む、接続指向のデバイスのみに関連します。 コネクションレス型デバイスは、これらのフィールドを 0 に設定する必要があります。

このメッセージは、リモートの NDIS デバイスは、次を示します。

-   最大リモート NDIS プロトコルのバージョン番号、デバイスをサポートできます。 結合されたバージョン番号はで、ホストを指定するバージョン番号未満にする必要があります、 [**リモート\_NDIS\_初期化\_MSG** ](remote-ndis-initialize-msg.md)メッセージ。 これにより、ホストがデバイスでサポートされているよりも小さいリモート NDIS プロトコルのバージョンを実装するときに、互換性モードにフォールバックするデバイスです。

-   デバイスが、ホストから受信する 1 つのデータ転送のバイトの最大サイズです。 デバイスは、各リモート NDIS メッセージに multimessage 転送の一部である必要があるバイトのアラインメントを指定できます。 2 の累乗では、この配置の値を指定します。 たとえばを 8 バイト アラインメントを示すために、3 にこの値を設定します。

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

 

 




