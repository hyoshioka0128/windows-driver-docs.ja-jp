---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY は、Wi-fi Direct のリセットが停止または再起動された後に、オペレーティングチャネルの選択のためにファームウェアによって使用されるポリシーを含む TLV です。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: caaae4ffc389879241c6ba5f9a6905d49aa5d2e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840445"
---
# <a name="wdi_tlv_p2p_go_internal_reset_policy"></a>WDI\_TLV\_P2P\_外出\_内部\_リセット\_ポリシー


WDI\_TLV\_P2P\_移動\_内部\_リセット\_ポリシーは、Wi-fi Direct のリセットが停止または再起動された後に、オペレーティングチャネルを選択するためにファームウェアによって使用されるポリシーを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xB2

## <a name="length"></a>Length


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| 種類                                                                                            | 説明                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_外出\_内部\_リセット\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_go_internal_reset_policy) (UINT32) | Wi-fi コンポーネント (たとえば、Bluetooth co ex 空間ストリームダウングレードなど) によって Wi-fi コンポーネントによって Wi-fi 直接移動が停止または再起動された場合、この構成によって、リセット後の動作チャネル選択のためにファームウェアによって適用されるポリシーが定義されます。 |

 

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

 

 




