---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS は、受信 Wi-fi ダイレクトアクションフレームパラメーターを含む TLV です。
ms.assetid: 8E530962-E4DC-4845-8A5F-87AC4E000DA8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 8569591efd1d490072287c6d3c736b902653ae25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842762"
---
# <a name="wdi_tlv_p2p_incoming_frame_parameters"></a>WDI\_TLV\_P2P\_受信\_フレーム\_パラメーター


WDI\_TLV\_P2P\_受信\_フレーム\_パラメーターは、受信した Wi-fi ダイレクトアクションフレームパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0X7a)

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                    | 説明                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 受信アクションフレームの型。             |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | リモートピアの MAC アドレス。                |
| UINT8                                                                   | トランザクションの Wi-fi ダイレクトダイアログトークン。 |

 

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

 

 




