---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY は、Wi-Fi Direct 移動リセットは停止して再起動した後、チャネルの選択を操作するために、ファームウェアによって使用されるポリシーを含む TLV です。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d0b49aed8609cee6d92ce59ecf1091ffed9d381f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579374"
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
| [**WDI\_P2P\_移動\_内部\_リセット\_ポリシー** ](https://msdn.microsoft.com/library/windows/hardware/dn926096) (UINT32) | 場合は、Wi-Fi Direct 移動リセットは、(たとえば、Bluetooth 共同 ex 空間ストリームのダウン グレード) を独自の IHV コンポーネントによって停止/再起動、この構成は、リセット後、チャネルの選択範囲を操作するためにファームウェアを採用するポリシーを定義します。 |

 

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

 

 




