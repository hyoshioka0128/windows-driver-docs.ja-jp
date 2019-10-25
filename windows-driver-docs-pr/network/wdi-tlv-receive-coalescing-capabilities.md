---
title: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES は、ハードウェア支援による受信フィルター機能を含む TLV です。
ms.assetid: 87BC1F55-90C6-4B22-9E8E-A54FF42515F3
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_COALESCING_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 07af62c5b7cf07ce9246558e9150125598b1a7a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843381"
---
# <a name="wdi_tlv_receive_coalescing_capabilities"></a>WDI\_TLV\_受信\_結合\_機能


WDI\_TLV は、ハードウェア支援による受信フィルター機能を含む TLV であり、\_の結合\_機能を\_ます。

## <a name="tlv-type"></a>TLV 型


0x9A

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>有効なフィルターの種類。 有効になっている受信フィルターの種類を指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VMQ_FILTERS_ENABLED</dt>
<dd><p>VMQ フィルターが有効であることを指定します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_FILTERS_ENABLED</dt>
<dd><p>NDIS パケット合体受信フィルターが有効であることを指定します。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>有効なキューの種類。 有効になっている受信キューの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUES_ENABLED</dt>
<dd><p>仮想マシン (VM) キューが有効であることを指定します。 VM キューは、ミニポートドライバーが VMQ インターフェイスを使用するように有効になっているときに使用されます。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>ネットワークアダプターがサポートする VM キューの数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている VM キューのプロパティ。 ネットワークアダプターがサポートする VM キュープロパティを指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MSI_X_SUPPORTED</dt>
<dd><p>ネットワークアダプターによって、各受信キューに対して MSI-X テーブルエントリが割り当てられました。 ネットワークアダプターでは、複数の受信キューに1つの MSI-X テーブルエントリを使用できません。 このフラグは、VMQ または sr-iov インターフェイスをサポートするミニポートドライバーでは必須です。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUE_SUPPORTED</dt>
<dd><p>VM キューのパケットフィルター処理をサポートするための最小要件は、ネットワークアダプターによって提供されます。 VMQ または sr-iov インターフェイスを使用できるようにするには、ミニポートドライバーでこのフラグを設定する必要があります。</p>
<p>VM キューパケットフィルターの VMQ 要件の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters" data-raw-source="[Setting and Clearing VMQ Filters](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)">Vmq フィルターの設定とクリア</a>」を参照してください。</p>
<p>VM キューパケットフィルターの SR-IOV 要件の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port" data-raw-source="[Setting a Receive Filter on a Virtual Port](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)">仮想ポートでの受信フィルターの設定</a>」を参照してください。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_LOOKAHEAD_SPLIT_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、受信した受信パケットを先読みオフセットで分割する VM キューをサポートします。 このオフセットは、要求された先読みサイズ以上です。 ネットワークアダプターは、DMA を使用して先読みおよび事後先読みデータを別々の共有メモリセグメントに転送します。</p>
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 このバージョンの NDIS をサポートするミニポートドライバーでは、このフラグを設定しないでください。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、次のいずれかのプロセッサアフィニティ属性を動的に変更する機能をサポートしています。</p>
<ul>
<li><p>VMQ インターフェイス内の VM キューのプロセッサ関係。 プロセッサの関係は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters" data-raw-source="[OID_RECEIVE_FILTER_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)">OID_RECEIVE_FILTER_QUEUE_PARAMETERS</a>の OID セット要求によって変更されます。</p></li>
<li><p>SR-IOV インターフェイスで作成され、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) に接続されている、既定以外の仮想ポート (VPort) のプロセッサアフィニティ。 プロセッサの関係は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters" data-raw-source="[OID_NIC_SWITCH_VPORT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)">OID_NIC_SWITCH_VPORT_PARAMETERS</a>の OID セット要求によって変更されます。</p></li>
</ul>
</dd>
<dt>NDIS_RECEIVE_FILTER_INTERRUPT_VECTOR_COALESCING_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、受信したパケットの割り込み合体を次のいずれかの方法でサポートします。</p>
<ul>
<li><p>VMQ インターフェイス内の複数の VM キュー。</p></li>
<li><p>SR-IOV インターフェイスの PF に接続されている複数の VPorts。</p></li>
</ul>
<p>このフラグが設定されている場合、ネットワークアダプターは、同じプロセッサアフィニティを持つ VM キューまたは VPorts の受信割り込みを結合する必要があります。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IMPLAT_MIN_OF_QUEUES_MODE</dt>
<dd><p>使用できる VM キューの数が、負荷分散フェールオーバー (LBFO) チームのどのメンバーからも使用できるキューの最小数であることを示します。 このフラグは、LBFO フィルターにのみ適用されます。 このフラグはミニポートに対して設定されていません。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IMPLAT_SUM_OF_QUEUES_MODE</dt>
<dd><p>使用可能な VM キューの数が、LBFO チームのすべてのメンバーが使用できるすべてのキューの合計であることを示します。 このフラグは、LBFO フィルターにのみ適用されます。 このフラグはミニポートに対して設定されていません。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_SUPPORTED_ON_DEFAULT_QUEUE</dt>
<dd><p>ネットワークアダプターは、NDIS パケット合体をサポートしています。 パケット合体は、ネットワークアダプターの既定の受信キューでのみサポートされています。 この受信キューには、NDIS_DEFAULT_RECEIVE_QUEUE_ID の識別子があります。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされているフィルターテスト。 ミニポートドライバーがサポートするテスト操作を指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_EQUAL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、選択したヘッダーフィールドのテストをサポートして、指定された値と等しいかどうかを判断します。</p>
<div class="alert">
<strong>注意</strong>  ミニポートドライバーが VMQ または sr-iov のインターフェイスをサポートしている場合は、このフラグを設定する必要があります。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_MASK_EQUAL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、選択されたヘッダーフィールドのマスク (ビットごとの AND) をサポートし、結果が指定された値と等しいかどうかを判断します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_NOT_EQUAL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、選択されたヘッダーフィールドのテストをサポートして、指定した値と等しくないかどうかを判断します。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされているヘッダー。 ミニポートドライバーが調べることができるネットワークパケットヘッダーの種類を指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ネットワークパケットのメディアアクセスコントロール (MAC) ヘッダーを調べることができます。 <strong>SupportedMacHeaderFields</strong>メンバーは、MAC ヘッダーから検査できるさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ネットワークパケットのアドレス解決プロトコル (ARP) ヘッダーを調べることができます。 <strong>SupportedArpHeaderFields</strong>メンバーは、ARP ヘッダーから検査できるさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV4_HEADER_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ネットワークパケットの IP version 4 (IPv4) ヘッダーを調べることができます。 <strong>SupportedIPv4HeaderFields</strong>メンバーは、IPv4 ヘッダーから検査できるさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV6_HEADER_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ネットワークパケットの IP version 6 (IPv6) ヘッダーを調べることができます。 <strong>SupportedIPv6HeaderFields</strong>メンバーは、IPv6 ヘッダーから検査できるさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_UDP_HEADER_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ネットワークパケットのユーザーデータグラムプロトコル (UDP) ヘッダーを調べることができます。 <strong>SupportedIPv6HeaderFields</strong>メンバーは、検査できる UDP ヘッダーのさまざまなフィールドを定義します。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている MAC ヘッダーフィールド。 ミニポートドライバーが調べることができる MAC ヘッダーフィールドの種類を指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_DEST_ADDR_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、MAC ヘッダーの宛先 MAC アドレスに基づく検査とフィルター処理をサポートしています。</p>
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降では、VMQ または sr-iov インターフェイスをサポートするミニポートドライバーで、このフラグを設定する必要があります。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SOURCE_ADDR_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、MAC ヘッダーのソース MAC アドレスに基づく検査とフィルター処理をサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、MAC ヘッダーの EtherType 識別子に基づく検査とフィルター処理をサポートしています。 たとえば、IPv4 パケットの EtherType 識別子は0x0800 です。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_VLAN_ID_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、MAC ヘッダーの VLAN 識別子に基づく検査とフィルター処理をサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PRIORITY_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、MAC ヘッダーの priority タグに基づく検査とフィルター処理をサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PACKET_TYPE_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、802.3 MAC ヘッダーの IEEE 802.2 サブネットワークアクセスプロトコル (スナップ) ヘッダーの [パケットの種類] フィールドに基づく検査とフィルター処理をサポートしています。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ミニポートドライバーがサポートする MAC ヘッダーフィルターの最大数。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最大キューグループ数。 この値は予約されています。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>キューグループあたりの最大キュー数。 この値は予約されています。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>ネットワークアダプターが先読みパケットバッファーに対してサポートする最小サイズ (バイト単位)。
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 このバージョンの NDIS をサポートするミニポートドライバーでは、このメンバーを0に設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ネットワークアダプターが先読みパケットバッファーに対してサポートする最大サイズ (バイト単位)。
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 このバージョンの NDIS をサポートするミニポートドライバーでは、このメンバーを0に設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている ARP ヘッダーフィールド。 ミニポートドライバーが調べることができる ARP ヘッダーフィールドの種類を指定するフラグのビットごとの OR。 次のフラグが有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_OPERATION_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ARP 操作フィールドでの受信フィルター処理をサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_SPA_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ARP ソースプロトコルアドレス (SPA) フィールドでの受信フィルター処理をサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_TPA_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、ARP ターゲットプロトコルアドレス (TPA) フィールドに対する受信フィルター処理をサポートしています。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている IPv4 ヘッダーフィールド。 ミニポートドライバーが調べることができる IPv4 ヘッダーフィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_IPV4_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、[IPv4 プロトコル] フィールドの受信フィルター処理をサポートしています。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている IPv6 ヘッダーフィールド。 ミニポートドライバーが検査できる IPv6 ヘッダーフィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_IPV6_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、[IPv6 プロトコル] フィールドの受信フィルター処理をサポートしています。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている UDP ヘッダーフィールド。 ミニポートドライバーが検査できる IPv6 ヘッダーフィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_UDP_HEADER_DEST_PORT_SUPPORTED</dt>
<dd><p>ネットワークアダプターは、[UDP 宛先ポート] フィールドでの受信フィルター処理をサポートしています。</p>
<div class="alert">
<strong>注</strong>  受信 UDP パケットに IPv4 オプションまたは IPv6 拡張ヘッダーが含まれている場合、ネットワークアダプターは、受信したパケットを自動的に削除し、udp フィルターテストに失敗したかのように処理できます。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>1つのパケット合体フィルターに指定できるパケットヘッダーフィールドに対するテストの最大数。 パケット合体の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing" data-raw-source="[NDIS Packet Coalescing](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)">NDIS パケット合体</a>」を参照してください。
<div class="alert">  
<strong>注</strong>パケット合体をサポートするネットワークアダプターは、1つのパケット合体フィルターに指定できる5つ以上のパケットヘッダーフィールドをサポートしている必要があります。 アダプターがパケット合体をサポートしていない場合、ミニポートドライバーはこの値を0に設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ネットワークアダプターによってサポートされるパケット合体受信フィルターの最大数。
<div class="alert">
<strong>注意</strong>  パケット合体をサポートするネットワークアダプターは、10個以上のパケット合体フィルターをサポートする必要があります。 アダプターがパケット合体をサポートしていない場合、ミニポートドライバーはこの値を0に設定する必要があります。
</div>
<div>
 
</div></td>
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
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_フィルター\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

 

 




