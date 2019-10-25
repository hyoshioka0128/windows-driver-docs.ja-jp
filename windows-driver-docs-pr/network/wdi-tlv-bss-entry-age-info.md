---
title: WDI_TLV_BSS_ENTRY_AGE_INFO
description: WDI_TLV_BSS_ENTRY_AGE_INFO は、BSS エントリの年齢情報を含む TLV です。
ms.assetid: 3D0DC599-2A66-45E9-B02C-32291A028139
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY_AGE_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 94399c2f9892d5fdeb02e77d4b0825a085b75d44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842876"
---
# <a name="wdi_tlv_bss_entry_age_info"></a>WDI\_TLV\_BSS\_エントリ\_AGE\_情報


WDI\_TLV\_BSS\_ENTRY\_AGE\_INFO は、BSS エントリの年齢情報を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xBA

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
<td>UINT64</td>
<td>この BSS エントリが最後に検出されたときのタイムスタンプ。 タイムスタンプは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentsystemtime" data-raw-source="[&lt;strong&gt;NdisGetCurrentSystemTime&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentsystemtime)"><strong>NdisGetCurrentSystemTime</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime" data-raw-source="[&lt;strong&gt;KeQuerySystemTime&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)"><strong>kequerysystemtime</strong></a>で取得する必要があります。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>この情報がライブである (現在実行中のスキャン中に検出される) か、または IHV コンポーネントの BSS リストキャッシュから取得されるかを指定します。
<p>有効な値は、0 (ライブ) または 1 (キャッシュ済み) です。</p></td>
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

 

 




