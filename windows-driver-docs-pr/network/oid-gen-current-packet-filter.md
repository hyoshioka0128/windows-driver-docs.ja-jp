---
title: OID_GEN_CURRENT_PACKET_FILTER
description: クエリとして、OID_GEN_CURRENT_PACKET_FILTER OID は、ミニポートドライバーから受信した通知のネットワークパケットの種類を報告します。
ms.assetid: d5a32626-caff-4708-a134-d80a845dee91
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_CURRENT_PACKET_FILTER
ms.localizationpriority: medium
ms.openlocfilehash: 2192a7a9733e1cdf18d0d788d371b7b25d0dd8a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837987"
---
# <a name="oid_gen_current_packet_filter"></a>OID\_GEN\_現在の\_パケット\_フィルター


クエリとして、OID\_GEN\_現在の\_パケット\_フィルター OID は、ミニポートドライバーから受信したネットワークパケットの種類を報告します。

設定として、OID\_GEN\_現在の\_パケット\_フィルター OID は、プロトコルがミニポートドライバーからの指示を受け取るネットパケットの種類を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
必ず. (「解説」を参照してください)

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a name="remarks"></a>注釈
-------

NDIS 6.0 以降のミニポートドライバーでは、クエリは要求されず、セットは必須です。 NDIS はミニポートドライバーのクエリを処理します。 ミニポートドライバーは、初期化中にパケットフィルター情報を報告します。

ミニポートドライバーは、その中の種類を、システムによってフィルターライブラリが提供されているものとして報告します。 パケットフィルターでは、または操作を使用して、次の型を結合します。

<a href="" id="ndis-packet-type-directed"></a>NDIS\_パケット\_種類\_ダイレクト  
ダイレクトパケット。 ダイレクトパケットには、NIC のステーションアドレスと同じ宛先アドレスが含まれます。

<a href="" id="ndis-packet-type-multicast"></a>NDIS\_パケット\_種類\_マルチキャスト  
マルチキャストアドレス一覧のアドレスに送信されたマルチキャストアドレスパケット。

プロトコルドライバーは、マルチキャストまたは機能アドレスのパケットの種類を指定することによって、イーサネット (802.3) マルチキャストパケットを受信できます。 マルチキャストアドレスの一覧または機能アドレスを設定すると、NIC ドライバーが有効にするマルチキャストアドレスグループが決まります。

<a href="" id="ndis-packet-type-all-multicast"></a>NDIS\_PACKET\_TYPE\_すべてのマルチキャスト\_  
マルチキャストアドレス一覧で列挙されたものだけでなく、すべてのマルチキャストアドレスパケット。

<a href="" id="ndis-packet-type-broadcast"></a>NDIS\_パケット\_種類\_ブロードキャスト  
ブロードキャストパケット。

<a href="" id="ndis-packet-type-promiscuous"></a>NDIS\_パケット\_種類\_無作為検出  
VLAN フィルターが有効になっているかどうか、および VLAN 識別子が一致するかどうかに関係なく、すべてのパケットを指定します。

<a href="" id="ndis-packet-type-all-functional"></a>NDIS\_PACKET\_TYPE\_すべての\_機能  
現在の機能アドレスのものだけでなく、すべての機能アドレスパケット。

<a href="" id="ndis-packet-type-all-local"></a>NDIS\_PACKET\_TYPE\_すべての\_ローカル  
インストールされているプロトコルと、指定された*NdisBindingHandle*によって識別される NIC によって示されるすべてのパケットによって送信されたすべてのパケット。

<a href="" id="ndis-packet-type-functional"></a>NDIS\_PACKET\_TYPE\_機能  
現在の機能アドレスに含まれるアドレスに送信される機能アドレスパケット。

<a href="" id="ndis-packet-type-group"></a>NDIS\_パケット\_種類\_グループ  
現在のグループアドレスに送信されたパケット。

<a href="" id="ndis-packet-type-mac-frame"></a>NDIS\_パケット\_種類\_MAC\_フレーム  
トークンリング NIC が受信する NIC ドライバーフレーム。

<a href="" id="ndis-packet-type-smt"></a>NDIS\_PACKET\_TYPE\_SMT  
FDDI NIC が受信する SMT パケット。

<a href="" id="ndis-packet-type-source-routing"></a>NDIS\_パケット\_種類\_ソース\_ルーティング  
すべてのソースルーティングパケット。 プロトコルドライバーがこのビットを設定した場合、NDIS ライブラリはソースルーティングブリッジとしての動作を試みます。

メディアの種類が**NdisMedium802\_3**または**NdisMedium802\_5**のミニポートアダプターの場合、NDIS は、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)関数の呼び出し中に、マルチキャストおよび機能アドレスと共に、パケットの受信を無効にします。

他のすべてのメディアの種類を使用するミニポートアダプターの場合、プロトコルドライバーは、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)の呼び出し中に、いつでもパケットの受信を開始できます。 プロトコルでは、 **NdisOpenAdapterEx**がを返す前にパケットを受信することもできます。 一般に、パケットフィルターは最適な作業であり、パケットフィルターが0の場合でも、受信の表示を処理できるようにプロトコルドライバーを準備する必要があります。

クエリの場合、NDIS は OR 演算子を使用して結合されたバインドフィルターを返します。

セットの場合、指定したパケットフィルターによって、バインドの前のパケットフィルターが置き換えられます。 ミニポートドライバーで以前にパケットの種類が有効になっていても、プロトコルドライバーでその種類が新しいフィルターで指定されていない場合、プロトコルドライバーはこの種類のパケットを受信しません。

メディアの種類が**NdisMedium802\_3**または**NdisMedium802\_5**のミニポートアダプターの場合、このクエリに応答して、ミニポートドライバーが特定のパケットの種類に対してビットを設定していないと、プロトコルドライバーはその種類のパケットを受信しません。 その結果、プロトコルドライバーは、0のフィルターを使用して[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)または[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出すことにより、パケットの受信を無効にすることができます。

他のすべてのメディアの種類を使用するミニポートアダプターの場合、NDIS はパケットの種類を確認しません。 これらのメディアの種類では、フィルター0を指定することによって、プロトコルドライバーでパケットの受信を無効にすることはできません。

ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ミニポートドライバーのパケットフィルターを0に設定する必要があります。 パケットフィルターが0の場合、受信通知は無効になります。 ミニポートドライバーの*MiniportInitializeEx*関数が返された後、プロトコルドライバーでは、OID\_GEN\_現在の\_パケット\_フィルターを0以外の値に設定できます。これにより、ミニポートドライバーは、そのプロトコルに対して受信したパケットを示すことができます。

\_パケット\_種類\_無作為検出を使用してプロミスカスモードが有効になっている場合、送信元のネットワークノードがパケットを受信していない場合でも、プロトコルドライバーはパケットを受信し続けます。 次に、NDIS は、NIC が受信するすべてのパケットをプロトコルドライバーに送信します。

特定のパケットフィルターを設定しても、同じ NIC にバインドされている他のプロトコルドライバーのパケットフィルターは変更されません。 たとえば、1つのバインドされたプロトコルで無作為検出モードが有効になっている場合、他のバインドされたプロトコルドライバーは、独自のパケットフィルターで特別に要求されていないパケットを受信しません。

**ネイティブ802.11 パケットフィルター**

ネイティブ802.11 ミニポートドライバーは、次の標準パケットフィルターの種類のみをサポートしている必要があります。

-   NDIS\_パケット\_種類\_ダイレクト

-   NDIS\_パケット\_種類\_マルチキャスト

-   NDIS\_パケット\_種類\_ブロードキャスト

-   NDIS\_パケット\_種類\_無作為検出

有効にすると、これらの標準パケットフィルターは802.11 データパケットにのみ適用されます。

また、ネイティブ802.11 ミニポートドライバーは、ネイティブ802.11 メディアに固有の次の種類のパケットフィルターをサポートしている必要があります。

<a href="" id="ndis-packet-type-802-11-raw-data"></a>NDIS\_PACKET\_TYPE\_802\_11\_生の\_データ  
802.11 メディアアクセスコントロール (MAC) プロトコルデータユニット (MPDU) フレーム。802.11 ステーションによって受信される形式のすべてのデータが含まれています。 このフィルターが設定されている場合、ドライバーは、MPDU フラグメントから再構築された MAC サービスデータユニット (MSDU) パケットを示す前に、変更されていないすべての MPDU フラグメントを示す必要があります。

MPDU フラグメントが暗号化されている場合、そのフラグメントが示される前に、そのフラグメントを復号化することはできません。 ただし、ミニポートドライバーは、reassembling を実行して MSDU パケットを示す前に、各 MPDU フラグメントの暗号化を解除する必要があります。

このフィルターの種類が有効になっている場合、NDIS\_PACKET\_TYPE\_有向または NDIS\_PACKET\_TYPE\_BROADCAST など、他の標準パケットフィルターにのみ影響します。

生の802.11 データパケットを示すメソッドの詳細については、「 [raw 802.11 パケットを示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-raw-802-11-packets)」を参照してください。

<a href="" id="ndis-packet-type-802-11-directed-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_ダイレクト\_管理  
指示された802.11 管理パケット。 ダイレクトパケットには、NIC のステーションアドレスと同じ宛先アドレスが含まれます。

<a href="" id="ndis-packet-type-802-11-multicast-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_マルチキャスト\_管理  
マルチキャストアドレス一覧のアドレスに送信されるマルチキャスト802.11 管理パケット。

<a href="" id="ndis-packet-type-802-11-all-multicast-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_すべての\_マルチキャスト\_管理  
802.11 MAC ヘッダーの宛先アドレスがマルチキャストアドレス一覧にあるかどうかに関係なく、802.11 ステーションによって受信されたすべてのマルチキャスト802.11 管理パケット。

<a href="" id="ndis-packet-type-802-11-broadcast-mgmt"></a>NDIS\_パケット\_種類\_802\_11\_ブロードキャスト\_管理  
802.11 ステーションによって受信された802.11 管理パケットをブロードキャストします。

<a href="" id="ndis-packet-type-802-11-promiscuous-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_無作為検出\_管理  
802.11 ステーションによって受信されたすべての802.11 管理パケット。

<a href="" id="ndis-packet-type-802-11-raw-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_RAW\_管理  
802.11 MPDU 管理フレーム。802.11 ステーションによって受信される形式のすべてのデータが含まれています。 このフィルターが設定されている場合、ドライバーは、MPDU フラグメントから再構築された MAC 管理プロトコルデータユニット (MMPDU) パケットを示す前に、変更されていないすべての MPDU フラグメントを示す必要があります。

有効にした場合、このフィルターの種類は、NDIS\_PACKET\_TYPE\_802\_11\_有向\_管理または NDIS\_パケット\_型\_802\_11\_マルチキャスト\_管理など、他の802.11 管理パケットフィルターにのみ影響します。

生の802.11 管理パケットを示すメソッドの詳細については、「 [raw 802.11 パケットを示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-raw-802-11-packets)」を参照してください。

<a href="" id="ndis-packet-type-802-11-directed-ctrl"></a>NDIS\_PACKET\_TYPE\_802\_11\_有向\_CTRL  
指示された802.11 制御パケット。 ダイレクトパケットには、NIC のステーションアドレスと同じ宛先アドレスが含まれます。

<a href="" id="ndis-packet-type-802-11-broadcast-ctrl"></a>NDIS\_PACKET\_TYPE\_802\_11\_BROADCAST\_CTRL  
ブロードキャスト802.11 は、802.11 ステーションによって受信されたパケットを制御します。

<a href="" id="ndis-packet-type-802-11-promiscuous-ctrl"></a>NDIS\_PACKET\_TYPE\_802\_11\_無作為検出\_CTRL  
802.11 ステーションによって受信されたすべての802.11 制御パケット。

ミニポートドライバーがネイティブ802.11 ネットワークモニター (NetMon) モードまたは拡張アクセスポイント (AP) モードで動作している場合、ドライバーは、OID\_GEN\_現在\_パケット\_フィルターのセット要求を使用して、次のパケットフィルターを有効にする必要があります。

-   NDIS\_パケット\_種類\_無作為検出

-   NDIS\_PACKET\_TYPE\_802\_11\_生の\_データ

-   NDIS\_PACKET\_TYPE\_802\_11\_無作為検出\_管理

-   NDIS\_PACKET\_TYPE\_802\_11\_RAW\_管理

-   NDIS\_PACKET\_TYPE\_802\_11\_無作為検出\_CTRL

NetMon 以外の他のネイティブ802.11 モードで動作するミニポートドライバーは、これらのパケットフィルター設定を有効にすることはできません。ただし、NDIS\_PACKET\_TYPE\_802\_11\_無作為検出\_CTRL を使用する必要があります。 NetMon モードで動作していないミニポートドライバーでは、必要に応じて、NDIS\_PACKET\_TYPE\_802\_11\_無作為検出を有効にすることができます。\_\_\_\_\_

**注  :** ミニポートドライバーが NetMon 以外のネイティブ802.11 モードであり、OID\_GEN\_現在の\_パケット\_フィルターが設定されている場合、oid データで無作為検出または未加工のフィルター設定が有効になっていると、ドライバーは set 要求を失敗させないようにする必要があります。

 

NetMon および ExtAP の動作モードの詳細については、次のトピックを参照してください。

[ネットワークモニター操作モード](https://docs.microsoft.com/windows-hardware/drivers/network/network-monitor-operation-mode)

[拡張可能なアクセスポイント操作モード](https://docs.microsoft.com/windows-hardware/drivers/network/extensible-access-point-operation-mode)

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)

 

 




