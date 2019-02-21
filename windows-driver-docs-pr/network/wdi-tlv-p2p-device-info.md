---
title: WDI_TLV_P2P_DEVICE_INFO
description: WDI_TLV_P2P_DEVICE_INFO では、Wi-Fi Direct デバイス情報を含む TLV です。
ms.assetid: 6B68F334-4C21-4088-AD47-9EB41F9A1CB8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4e61453cab034cd04021aa4151560da2dc1ee950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550520"
---
# <a name="wditlvp2pdeviceinfo"></a>WDI\_TLV\_P2P\_デバイス\_情報


WDI\_TLV\_P2P\_デバイス\_情報は、Wi-Fi Direct デバイス情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x96

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_DEVICE\_INFO\_PARAMETERS**](wdi-tlv-p2p-device-info-parameters.md) |                                |          | デバイスについては、Wi-Fi Direct デバイスのアドレス、構成がサポートされているメソッドでは、プライマリ デバイスの種類など。 |
| [**WDI\_TLV\_P2P\_デバイス\_名**](wdi-tlv-p2p-device-name.md)                        |                                |          | このデバイスのデバイスの名前。                                                                                         |

 

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

 

 




