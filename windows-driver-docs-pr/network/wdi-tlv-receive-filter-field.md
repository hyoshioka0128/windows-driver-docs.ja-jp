---
title: WDI_TLV_RECEIVE_FILTER_FIELD (0x65)
description: WDI_TLV_RECEIVE_FILTER_FIELD は、ネットワークヘッダーの1つのフィールドに対する受信フィルターのテスト条件を含む TLV です。
ms.assetid: 9037CD08-742E-4A99-A37B-9969A2BC666A
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_FILTER_FIELD (0x65) Windows Vista 以降のネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 6f73f8212e171874fdc7a475bcb315314d4167a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842272"
---
# <a name="wdi_tlv_receive_filter_field-0x65"></a>WDI\_TLV\_RECEIVE\_FILTER\_フィールド (0x65)


WDI\_TLV\_RECEIVE\_FILTER\_FIELD は、ネットワークヘッダーの1つのフィールドの受信フィルターテスト条件を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x65

## <a name="length"></a>Length


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>フラグのビットごとの OR を指定します。 使用可能なフラグ値は WDI_RECEIVE_FILTER_FIELD_MAC_HEADER_VLAN_UNTAGGED_OR_ZERO です。 このフラグが設定されている場合、ネットワークアダプターは次の条件を満たす受信パケットのみを示す必要があります。
<ul>
<li>パケットの MAC アドレスは、指定された MAC ヘッダーフィールドのテストに一致します。</li>
<li>パケットに VLAN タグが含まれていないか、ID が0の VLAN タグがあります。</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_frame_header" data-raw-source="[&lt;strong&gt;NDIS_FRAME_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_frame_header)"><strong>NDIS_FRAME_HEADER</strong></a> (UINT32)</td>
<td>フレームヘッダー。 フレームヘッダーの種類を指定します。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_test" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_TEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_test)"><strong>NDIS_RECEIVE_FILTER_TEST</strong></a> (UINT32)</td>
<td>受信フィルターテスト。 受信フィルターが実行するテストの種類を指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ヘッダーフィールド。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>で説明されているように、共用体を使用してプロトコル固有のヘッダーフィールドの種類を指定します。HeaderField。</td>
</tr>
<tr class="odd">
<td>UINT8 [16]</td>
<td>フィールド値。 ミニポートアダプターが受信パケットの対応するヘッダーフィールド値と比較する値を指定します。 ヘッダーフィールドの値の場所は、<em>ヘッダーフィールド</em>要素で指定されているフィールドの種類によって決まります。 この値はネットワークのバイト順であり、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>に記載されているように、共用体で指定されます。FieldValue.</td>
</tr>
<tr class="even">
<td>UINT8 [16]</td>
<td>テスト結果の値。 <em>受信フィルターテスト</em>要素が Receivefiltertestマスク kequal に設定されている場合、ネットワークアダプターは、まず、<em>フィールド値</em>メンバーの値と、<em>ヘッダーフィールド</em>メンバーで指定されたヘッダーフィールド値の結果を計算します。 次に、アダプターは、計算された結果と<em>結果値</em>を比較します。 この値は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>に記載されているように、共用体で指定します。ResultValue。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




