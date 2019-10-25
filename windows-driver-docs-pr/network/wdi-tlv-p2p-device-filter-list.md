---
title: WDI_TLV_P2P_DEVICE_FILTER_LIST
description: WDI_TLV_P2P_DEVICE_FILTER_LIST は、wi-fi ダイレクトデバイスの検出中に検索する Wi-fi ダイレクトデバイスとグループ所有者の一覧を含む TLV です。
ms.assetid: 56D1E6BD-41E3-4869-A821-334012B781A7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_FILTER_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e17c70cd8c97dcfdc78c8920fb44b97f7efe24ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840452"
---
# <a name="wdi_tlv_p2p_device_filter_list"></a>WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧


WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧は、wi-fi direct デバイスの検出中に検索する Wi-fi ダイレクトデバイスとグループ所有者の一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>Length


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| 種類                                                  | 説明                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-fi ダイレクトデバイスの検出中に検索する Wi-fi ダイレクトデバイスとグループの所有者の一覧。 |

 

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

 

 




