---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS は、Wi-fi ダイレクトの構成方法を含む TLV です。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CONFIG_METHODS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: a970603ab40ea577bbcf14afc5935d0c69a7df17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840456"
---
# <a name="wdi_tlv_p2p_config_methods"></a>WDI\_TLV\_P2P\_CONFIG\_メソッド


WDI\_TLV\_P2P\_CONFIG\_メソッドは、Wi-fi ダイレクトの構成方法を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xEB

## <a name="length"></a>Length


UINT16 のサイズ (バイト単位)。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | [**WDI\_WPS\_構成\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)で定義されている構成方法。 ピンの表示、ピンパッド、およびその他の場合にのみ適用できます。 |

 

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

 

 




