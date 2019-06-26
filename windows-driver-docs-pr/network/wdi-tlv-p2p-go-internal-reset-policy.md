---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY は、Wi-Fi Direct 移動リセットは停止して再起動した後、チャネルの選択を操作するために、ファームウェアによって使用されるポリシーを含む TLV です。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9c7705c3f3cc713f2b3661a7f147a395bcf70bd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384197"
---
# <a name="wditlvp2pgointernalresetpolicy"></a>WDI\_TLV\_P2P\_移動\_内部\_リセット\_ポリシー


WDI\_TLV\_P2P\_移動\_内部\_リセット\_ポリシーは、Wi-Fi Direct 移動リセットが停止した後、チャネルの選択を操作するために、ファームウェアによって使用されるポリシーを含む TLV/再起動します。

## <a name="tlv-type"></a>TLV 型


0xB2

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型                                                                                            | 説明                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_移動\_内部\_リセット\_ポリシー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_go_internal_reset_policy) (UINT32) | 場合は、Wi-Fi Direct 移動リセットは、(たとえば、Bluetooth 共同 ex 空間ストリームのダウン グレード) を独自の IHV コンポーネントによって停止/再起動、この構成は、リセット後、チャネルの選択範囲を操作するためにファームウェアを採用するポリシーを定義します。 |

 

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

 

 




