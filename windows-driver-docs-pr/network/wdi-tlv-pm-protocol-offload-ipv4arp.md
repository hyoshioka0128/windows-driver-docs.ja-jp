---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP では、IPv4 ARP プロトコルを含む TLV は、パラメーターをオフロードします。
ms.assetid: 03894B22-3D4B-4262-893A-660FC88AA93D
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0b0d4692c2177801f6eec6d5a4f1725b510e560c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527778"
---
# <a name="wditlvpmprotocoloffloadipv4arp"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP


WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP は IPv4 ARP プロトコルのオフロード パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x61

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                                                                                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | プロトコルのオフロード ID を指定します これは、オフロードされたプロトコルを識別する OS で提供される値です。 OS では、追加要求を送信します。 または、上にあるドライバーへの要求が完了すると、前に、プロトコル間で一意の値に OS セット ProtocolOffloadId をネットワーク アダプターにオフロードします。                                                                   |
| UINT8\[4\]                                        | ARP 要求のソース プロトコル アドレス (SPA) フィールドと一致する省略可能な IPv4 アドレスを指定します。 受信の ARP 要求にこの IPv4 アドレスに一致する SPA 値がある場合は、ネットワーク アダプターは、低電力状態にあるときに、ARP 応答を送信します。 これは、0 に設定されている場合、ネットワーク アダプターは、リモートの IPv4 アドレスから ARP 要求に応答します。 |
| UINT8\[4\]                                        | ARP 応答を送信するときに、ソース プロトコル アドレス (SPA) フィールドのネットワーク アダプターを使用してホストの IPv4 アドレスを指定します。                                                                                                                                                                                                                                            |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 生成される ARP 応答パケットのソース ハードウェア アドレス (SHA) フィールドを使用する必要があります、ネットワーク アダプター MAC アドレスを指定します。 ただし、MAC ヘッダーの送信元アドレスとして、ネットワーク アダプターの現在の MAC アドレスを使用してください。                                                                                                          |

 

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

 

 




