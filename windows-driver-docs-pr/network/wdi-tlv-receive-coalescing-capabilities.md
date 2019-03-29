---
title: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES は、ハードウェア支援によるを含む TLV は、フィルター機能を利用します。
ms.assetid: 87BC1F55-90C6-4B22-9E8E-A54FF42515F3
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_COALESCING_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c7d1434689d85916a941568db6b644998891b623
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582224"
---
# <a name="wditlvreceivecoalescingcapabilities"></a>WDI\_TLV\_受信\_COALESCING\_機能


WDI\_TLV\_受信\_COALESCING\_機能は、ハードウェア支援によるを含む TLV は、フィルター機能を利用します。

## <a name="tlv-type"></a>TLV 型


0x9A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>フィルターの種類を有効になります。 有効になっている受信フィルターの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VMQ_FILTERS_ENABLED</dt>
<dd><p>VMQ フィルターが有効になっていることを指定します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_FILTERS_ENABLED</dt>
<dd><p>NDIS パケットの結合フィルターが表示されることを指定します。 有効にします。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>有効なキューの種類。 有効になっている受信キューの型を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUES_ENABLED</dt>
<dd><p>仮想マシン (VM) のキューが有効になっていることを指定します。 VMQ インターフェイスを使用するミニポート ドライバーが有効にすると、VM のキューが使用されます。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>ネットワーク アダプターをサポートする VM のキューの数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>VM サポートされているキューのプロパティ。 ネットワーク アダプターをサポートする VM のキューのプロパティを指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MSI_X_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、受信キューごとに、MSI X テーブルのエントリが割り当てられます。 ネットワーク アダプターの複数の受信キュー MSI X テーブル エントリが 1 つを使用する必要があります。 このフラグは、VMQ または SR-IOV インターフェイスをサポートするミニポート ドライバーに対して必須です。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUE_SUPPORTED</dt>
<dd><p>ネットワーク アダプターでは、VM キュー パケットのフィルター処理をサポートする最小要件を提供します。 VMQ または SR-IOV インターフェイスを使用する有効な場合、ミニポート ドライバーはこのフラグを設定する必要があります。</p>
<p>VM キュー パケットのフィルター処理するために VMQ 要件の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff570780" data-raw-source="[Setting and Clearing VMQ Filters](https://msdn.microsoft.com/library/windows/hardware/ff570780)">設定および VMQ のフィルターをクリアする</a>します。</p>
<p>VM キュー パケットのフィルター処理するための SR-IOV 要件の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh440224" data-raw-source="[Setting a Receive Filter on a Virtual Port](https://msdn.microsoft.com/library/windows/hardware/hh440224)">仮想ポートで受信フィルターを設定</a>します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_LOOKAHEAD_SPLIT_SUPPORTED</dt>
<dd><p>ネットワーク アダプターでは、VM キュー先読みオフセット入力方向の受信パケットの分割をサポートしています。 このオフセットは先読みアサーションが要求されたサイズ以上です。 ネットワーク アダプターでは、DMA を使用して、共有メモリ セグメントを区切る先読みアサーションと後先読みのデータを転送します。</p>
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 サポートのこのバージョンの NDIS ミニポート ドライバーでは、このフラグは設定しない必要があります。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、次のプロセッサ アフィニティ属性のいずれかを動的に変更する機能がサポートされています。</p>
<ul>
<li><p>VMQ インターフェイスで VM のキューのプロセッサ アフィニティ。 プロセッサのアフィニティは、の OID セットの要求によって変更される<a href="https://msdn.microsoft.com/library/windows/hardware/ff569794" data-raw-source="[OID_RECEIVE_FILTER_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569794)">OID_RECEIVE_FILTER_QUEUE_PARAMETERS</a>します。</p></li>
<li><p>SR-IOV インターフェイスで作成されており、PCI Express (PCIe) 物理機能 (PF) のネットワーク アダプターに関連付けられている既定以外仮想ポート (VPort) のプロセッサ アフィニティ。 プロセッサのアフィニティは、の OID セットの要求によって変更される<a href="https://msdn.microsoft.com/library/windows/hardware/hh451825" data-raw-source="[OID_NIC_SWITCH_VPORT_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451825)">OID_NIC_SWITCH_VPORT_PARAMETERS</a>します。</p></li>
</ul>
</dd>
<dt>NDIS_RECEIVE_FILTER_INTERRUPT_VECTOR_COALESCING_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、割り込みは、次のいずれかで受信したパケットの結合がサポートされています。</p>
<ul>
<li><p>VMQ インターフェイスで複数の VM のキュー。</p></li>
<li><p>SR-IOV インターフェイスで PF にアタッチされている複数の拡張。</p></li>
</ul>
<p>このフラグが設定されている場合、ネットワーク アダプターに結合する必要がありますの VM のキューまたは拡張を同じプロセッサ アフィニティを持つ割り込みを受信します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IMPLAT_MIN_OF_QUEUES_MODE</dt>
<dd><p>使用できる VM のキューの数が負荷分散フェールオーバー (LBFO) チームのメンバーから使用できるキューの最小数であることを示します。 このフラグは、LBFO フィルターのみに適用されます。 ミニポートは、このフラグは設定されていません。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_IMPLAT_SUM_OF_QUEUES_MODE</dt>
<dd><p>使用できる VM のキューの数は、LBFO チームのすべてのメンバーから使用できるすべてのキューの合計であることを示します。 このフラグは、LBFO フィルターのみに適用されます。 ミニポートは、このフラグは設定されていません。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_SUPPORTED_ON_DEFAULT_QUEUE</dt>
<dd><p>ネットワーク アダプターでは、NDIS パケットの結合をサポートします。 既定のパケットの結合はサポートされてのみのネットワーク アダプターのキューを受信します。 この受信キューでは、NDIS_DEFAULT_RECEIVE_QUEUE_ID の識別子を保持します。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>フィルターのテストがサポートされています。 ミニポート ドライバーがサポートするテストの操作を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_EQUAL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターでは、指定された値と等しいかどうかを選択したヘッダー フィールドのテストをサポートします。</p>
<div class="alert">
<strong>注</strong>  ミニポート ドライバーでは、VMQ または SR-IOV インターフェイスをサポートする場合、前に、このフラグを設定する必要があります。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_MASK_EQUAL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、結果が指定値と等しいかどうかを選択したヘッダー フィールドのマスク (つまり、ビット演算 AND) がサポートしています。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_NOT_EQUAL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターでは、選択したヘッダー フィールドが指定された値と等しくないかどうかを判断するテストをサポートします。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされているヘッダー。 ミニポート ドライバーを検査できるネットワーク パケット ヘッダーの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、ネットワーク パケットのメディア アクセス制御 (MAC) ヘッダーを検査できます。 <strong>SupportedMacHeaderFields</strong>メンバーが調査できる MAC ヘッダーからさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、ネットワーク パケットのアドレス解決プロトコル (ARP) ヘッダーを検査できます。 <strong>SupportedArpHeaderFields</strong>メンバーが参照できる ARP ヘッダーからさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV4_HEADER_SUPPORTED</dt>
<dd><p>ネットワーク アダプターが IP version 4 (IPv4) を検査、ネットワーク パケットのヘッダー。 <strong>SupportedIPv4HeaderFields</strong>メンバーが調査できる IPv4 ヘッダーからさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV6_HEADER_SUPPORTED</dt>
<dd><p>ネットワーク アダプターが IP version 6 (IPv6) を検査、ネットワーク パケットのヘッダー。 <strong>SupportedIPv6HeaderFields</strong>メンバーが調査できる IPv6 ヘッダーからさまざまなフィールドを定義します。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_UDP_HEADER_SUPPORTED</dt>
<dd><p>ネットワーク アダプターには、ネットワーク パケットのユーザー データグラム プロトコル (UDP) ヘッダーを検査できます。 <strong>SupportedIPv6HeaderFields</strong>メンバーが調査できる UDP ヘッダーからさまざまなフィールドを定義します。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている MAC ヘッダー フィールド。 ミニポート ドライバーを検査できる MAC ヘッダー フィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_DEST_ADDR_SUPPORTED</dt>
<dd><p>検査およびフィルター処理するネットワーク アダプターのサポートは、接続先 MAC ヘッダーで MAC アドレスに基づいています。</p>
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降、VMQ または SR-IOV インターフェイスをサポートするミニポート ドライバーはこのフラグを設定する必要があります。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SOURCE_ADDR_SUPPORTED</dt>
<dd><p>ネットワーク アダプターはサポートを検査およびフィルター処理、ソース MAC ヘッダーの MAC アドレスに基づくします。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターがサポートを検査およびフィルタ リング MAC ヘッダーで EtherType 識別子に基づく。 たとえば、IPv4 パケットの EtherType 識別子は、0x0800 は。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_VLAN_ID_SUPPORTED</dt>
<dd><p>ネットワーク アダプターがサポートを検査およびフィルタ リング MAC ヘッダーで VLAN 識別子に基づく。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PRIORITY_SUPPORTED</dt>
<dd><p>ネットワーク アダプターがサポートを検査およびフィルタ リング MAC ヘッダーの優先順位のタグに基づく。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PACKET_TYPE_SUPPORTED</dt>
<dd><p>検査およびフィルター処理するは、IEEE 802.2 サブネットワーク アクセス プロトコルのパケットの type フィールドに基づくはネットワーク アダプターのサポートは、802.3 MAC ヘッダーにヘッダーを (スナップ)。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ミニポート ドライバーがサポートする MAC ヘッダー フィルターの最大数。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>キューの最大のグループ。 この値は予約されています。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>キュー グループあたりの最大キュー。 この値は予約されています。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>バイト単位の先読みパケット バッファーのネットワーク アダプターをサポートする最小サイズ。
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 このバージョンの NDIS をサポートするミニポート ドライバーは、このメンバーを 0 に設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ネットワーク アダプターのサポートの先読みパケット バッファーをバイト単位で最大サイズ。
<div class="alert">
<strong>注</strong>  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 このバージョンの NDIS をサポートするミニポート ドライバーは、このメンバーを 0 に設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている ARP ヘッダー フィールド。 ミニポート ドライバーを検査できる ARP ヘッダー フィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_OPERATION_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートは、ARP 操作のフィールドをフィルター処理を受け取ります。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_SPA_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートでは、ARP ソース プロトコルのアドレス (SPA) フィールドをフィルター処理を受信します。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_TPA_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートは、ARP ターゲット プロトコルのアドレス (TPA) フィールドをフィルター処理を受け取ります。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている IPv4 ヘッダー フィールド。 ミニポート ドライバーを検査できる IPv4 ヘッダー フィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV4_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートは、IPv4 プロトコル フィールドをフィルター処理を受信します。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている IPv6 ヘッダー フィールド。 ミニポート ドライバーを検査できる IPv6 ヘッダー フィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV6_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートは、IPv6 プロトコル フィールドをフィルター処理を受信します。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている UDP ヘッダー フィールド。 ミニポート ドライバーを検査できる IPv6 ヘッダー フィールドの種類を指定するフラグのビットごとの OR。 次のフラグは有効です。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_UDP_HEADER_DEST_PORT_SUPPORTED</dt>
<dd><p>ネットワーク アダプターのサポートでは、UDP 宛先ポート フィールドをフィルター処理を受信します。</p>
<div class="alert">
<strong>注</strong>  ネットワーク アダプターの受信パケットを削除して UDP フィルターのテストに失敗したかのように扱うことできます自動的に受信 UDP パケットにオプションの IPv4 または IPv6 拡張ヘッダーが含まれる場合。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>1 つのパケットの結合フィルターのパケット ヘッダー フィールドに指定できるテストの最大数。 パケットの結合の詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451601" data-raw-source="[NDIS Packet Coalescing](https://msdn.microsoft.com/library/windows/hardware/hh451601)">NDIS パケット結合</a>します。
<div class="alert">
<strong>注</strong>  パケットの結合をサポートするネットワーク アダプターが 1 つのパケットの結合フィルターの指定できる 5 つ以上のパケット ヘッダー フィールドをサポートする必要があります。 アダプターがパケットの結合をサポートしていない場合、ミニポート ドライバーは 0 にこの値を設定する必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>パケットの結合の最大数には、ネットワーク アダプターでサポートされているフィルターが表示されます。
<div class="alert">
<strong>注</strong>  パケットの結合をサポートするネットワーク アダプターが 10 個以上のパケットの結合フィルターをサポートする必要があります。 アダプターがパケットの結合をサポートしていない場合、ミニポート ドライバーは 0 にこの値を設定する必要があります。
</div>
<div>
 
</div></td>
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
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

 

 




