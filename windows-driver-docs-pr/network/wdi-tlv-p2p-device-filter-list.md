---
title: WDI_TLV_P2P_DEVICE_FILTER_LIST
description: WDI_TLV_P2P_DEVICE_FILTER_LIST は、Wi-Fi Direct デバイスの検出中に検索するには、Wi-Fi Direct デバイスの一覧を含む TLV とグループの所有者です。
ms.assetid: 56D1E6BD-41E3-4869-A821-334012B781A7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_FILTER_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e90369d8c488671416b8808bc037b28764501f7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355105"
---
# <a name="wditlvp2pdevicefilterlist"></a>WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧


WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧は、Wi-Fi Direct デバイスの検出中に検索するには、Wi-Fi Direct デバイスの一覧を含む TLV とグループの所有者。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 型                                                  | 説明                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-Fi Direct デバイスと Wi-Fi Direct デバイスの検出中に検索するグループの所有者の一覧。 |

 

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

 

 




