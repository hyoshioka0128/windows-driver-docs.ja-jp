---
title: WDI_TLV_AP_BAND_CHANNEL
description: WDI_TLV_AP_BAND_CHANNEL では、アクセス ポイントのバンドとチャネル情報を指定する TLV です。
ms.assetid: 5659CFA1-7FA9-490D-83DE-A56A895602A0
ms.date: 07/18/2017
keywords:
- WDI_TLV_AP_BAND_CHANNEL ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2c6031d0c01206720563b9e8a9d8df2fccea37d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353621"
---
# <a name="wditlvapbandchannel"></a>WDI\_TLV\_AP\_バンド\_チャネル


WDI\_TLV\_AP\_バンド\_チャネルは、アクセス ポイントのバンドとチャネル情報を指定する TLV します。

**注**  この TLV は、Windows 10 バージョン 1511、WDI バージョン 1.0.10 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x127

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                |
|--------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI\_TLV\_BANDID**](wdi-tlv-bandid.md)                         |                                |          | バンドの識別子を指定します。                     |
| [**WDI\_TLV\_チャネル\_情報\_一覧**](wdi-tlv-channel-info-list.md) |                                | x        | アクセス ポイントを開始するチャネルのリストを指定します。 |

 

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


[OID\_WDI\_タスク\_開始\_アジア太平洋](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap)

 

 




