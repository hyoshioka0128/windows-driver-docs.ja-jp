---
title: WDI_TLV_ADDITIONAL_IES
description: WDI_TLV_ADDITIONAL_IES では、その他の要素 (IE) の設定を含む TLV です。
ms.assetid: B9094E9D-894F-4B23-B4DA-126F87E908C9
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADDITIONAL_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b9435f3958ae96bf91457b629d5ab9e80c9e5e21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570644"
---
# <a name="wditlvadditionalies"></a>WDI\_TLV\_追加\_IES


WDI\_TLV\_追加\_IES は追加の要素 (IE) の設定を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x8A

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                                                                          |
|------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_追加\_ビーコン\_IES**](wdi-tlv-additional-beacon-ies.md)                                 |                                | x        | ビーコン IEs の配列。 Wi-Fi Direct のポートはグループの所有者として動作しているときにビーコン パケットにこれらの追加 IEs を追加する必要があります。 これには、Wi-Fi Direct のポートはデバイスまたはクライアントのモードで動作しているときは無視されます。                                                                                              |
| [**WDI\_TLV\_追加\_プローブ\_応答\_IES**](wdi-tlv-additional-probe-response-ies.md)                |                                | x        | プローブの応答での配列。 Wi-Fi Direct のポートは、Wi-Fi Direct デバイスまたはグループの所有者として動作しているときに、プローブ応答パケットをこれら追加 IEs を追加する必要があります。 これには、Wi-Fi Direct のポートは、クライアント モードで動作している場合は無視されます。                                                                 |
| [**WDI\_TLV\_ADDITIONAL\_PROBE\_REQUEST\_DEFAULT\_IES**](wdi-tlv-additional-probe-request-default-ies.md) |                                | x        | その他のプローブ要求 IEs の配列。 このオフセットは、この構造体を格納しているバッファーの先頭からの相対です。 Wi-Fi Direct のポートでは、これらの追加 IEs をで送信されたプローブ要求パケットに追加する必要があります。 Wi-Fi Direct 検出する要求で上書きできる既定のプローブ要求 IEs に注意してください。 |

 

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

 

 




