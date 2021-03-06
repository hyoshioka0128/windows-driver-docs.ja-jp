---
title: WDI_TLV_RECEIVE_FILTER_FIELD (0x65)
description: WDI_TLV_RECEIVE_FILTER_FIELD は、受信フィルターを含む TLV は、ネットワーク ヘッダーの 1 つのフィールドの条件をテストします。
ms.assetid: 9037CD08-742E-4A99-A37B-9969A2BC666A
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_FILTER_FIELD (0x65) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 772caf5d21d87076f9bf7b84f95ee95e6f6405a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376992"
---
# <a name="wditlvreceivefilterfield-0x65"></a>WDI\_TLV\_受信\_フィルター\_フィールド (0x65)


WDI\_TLV\_受信\_フィルター\_フィールドがフィールド ネットワーク ヘッダーを 1 つの受信フィルター テスト条件を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x65

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
<td>フラグのビットごとの OR を指定します。 可能なフラグ値は、WDI_RECEIVE_FILTER_FIELD_MAC_HEADER_VLAN_UNTAGGED_OR_ZERO です。 このフラグが設定されている場合、ネットワーク アダプターはのみ、次の条件に合格した受信パケット数を示す必要があります。
<ul>
<li>パケットの MAC アドレスでは、MAC ヘッダー フィールドの指定したテストと一致します。</li>
<li>パケットは、VLAN タグが含まれていないか、または id が 0 の VLAN タグがあります。</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_frame_header" data-raw-source="[&lt;strong&gt;NDIS_FRAME_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_frame_header)"><strong>NDIS_FRAME_HEADER</strong> </a> (UINT32)</td>
<td>フレームのヘッダー。 フレームのヘッダーの種類を指定します。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_receive_filter_test" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_TEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_receive_filter_test)"><strong>NDIS_RECEIVE_FILTER_TEST</strong> </a> (UINT32)</td>
<td>フィルターのテストが表示されます。 受信フィルターを実行するテストの種類を指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ヘッダー フィールド。 記載されているように、union と共に、プロトコル固有のヘッダー フィールドの種類を指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>します。HeaderField します。</td>
</tr>
<tr class="odd">
<td>UINT8[16]</td>
<td>フィールドの値。 ミニポート アダプターが受信パケットに対応するヘッダー フィールドの値を比較する値を指定します。 ヘッダー フィールド値の場所がで指定されているフィールドの種類によって決まりますが、<em>ヘッダー フィールド</em>要素。 この値は、ネットワークのバイト順に記載されている和集合を指定した、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>します。FieldValue します。</td>
</tr>
<tr class="even">
<td>UINT8[16]</td>
<td>テスト結果の値です。 場合、<em>受信フィルター テスト</em>ReceiveFilterTestMaskEqual に要素が設定されている、ネットワーク アダプターが最初の値からの結果を計算、<em>フィールドの値</em>メンバーと、ヘッダー フィールドの指定された値によって、<em>ヘッダー フィールド</em>メンバー。 アダプターで、計算結果を比較<em>値を結果</em>します。 記載されている和集合でこの値が指定されて、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>します。ResultValue します。</td>
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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




