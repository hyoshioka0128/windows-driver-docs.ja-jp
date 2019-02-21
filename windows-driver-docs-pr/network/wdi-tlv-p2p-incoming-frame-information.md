---
title: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION
description: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION では、受信の Wi-Fi Direct アクション フレーム情報を含む TLV です。
ms.assetid: 7E7EF56D-625B-4B79-9AE4-A9C9B7C8547A
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCOMING_FRAME_INFORMATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9fc6067b325e4778a6cfe4e0c2fd09b9be2ca9cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538376"
---
# <a name="wditlvp2pincomingframeinformation"></a>WDI\_TLV\_P2P\_受信\_フレーム\_情報


WDI\_TLV\_P2P\_受信\_フレーム\_情報は、受信の Wi-Fi Direct アクション フレーム情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x79

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_受信\_フレーム\_パラメーター**](wdi-tlv-p2p-incoming-frame-parameters.md) |                                |          | 受信のフレームのパラメーターを指定します。                                                                                                                                                                                        |
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_IES**](wdi-tlv-p2p-action-frame-ies.md)                   |                                |          | 公開操作を受信したフレームの IEs セクションを指定します。                                                                                                                                                                  |
| [**WDI\_TLV\_ACTION\_FRAME\_DEVICE\_CONTEXT**](wdi-tlv-action-frame-device-context.md)     |                                | X        | この受信メッセージに応答を送信するホストが決定した場合、元に戻す渡されるベンダー固有の情報を指定します。 有効期間管理を回避するためには、問題と、IHV コンポーネントは、このフィールドにポインターを使用しない必要があります。 |

 

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

 

 




