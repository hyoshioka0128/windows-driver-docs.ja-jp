---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS では、IPv6 NS プロトコルを含む TLV は、パラメーターをオフロードします。
ms.assetid: 0385449B-82C6-44B4-BBD3-A708ADE54AC4
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0c8ddc5377c4fe41503085ca4a018b9e315cce9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362960"
---
# <a name="wditlvpmprotocoloffloadipv6ns"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS


WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS は IPv6 NS プロトコルのオフロード パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x62

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | プロトコルのオフロード ID を指定します これは、オフロードされたプロトコルを識別する OS で提供される値です。 OS では、追加要求を送信します。 または、上にあるドライバーへの要求が完了すると、前に、プロトコル間で一意の値に OS セット ProtocolOffloadId をネットワーク アダプターにオフロードします。                                                                                                    |
| UINT8\[16\]                                       | NS メッセージの IPv6 ヘッダーの送信元アドレス フィールドと一致する省略可能な IPv6 アドレスを指定します。 NS の受信メッセージがある発信元アドレスの値 (NA) 近隣通知メッセージの省電力状態にあるときにネットワーク アダプターは、この IPv6 アドレスと一致します。 これは、0 に設定されている場合、リモートの IPv6 アドレスから、ネットワーク アダプターが NS メッセージに応答する必要があります。 |
| UINT8\[16\]                                       | 要請されたノードの IPv6 アドレスを指定します。                                                                                                                                                                                                                                                                                                                                                                     |
| UINT8\[16\]                                       | NS の受信メッセージのターゲット アドレス フィールドに一致する 1 つまたは 2 つの IPv6 アドレスを指定します。 1 つのアドレスがある場合は、ターゲット アドレスを 1 にそのアドレスが格納されているし、ターゲット アドレス 2 がゼロで埋められました。 これらのアドレスのいずれかには、NS の受信メッセージのターゲット アドレス フィールドが一致すると、ネットワーク アダプターは、応答で NA メッセージを送信します。                                               |
| UINT8\[16\]                                       | ターゲット アドレス 1 の説明を参照してください。                                                                                                                                                                                                                                                                                                                                                                           |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 生成される NA メッセージのターゲットのリンク層アドレス (TLLA) フィールドのネットワーク アダプターを使用する必要がある MAC アドレスを指定します。 ただし、MAC ヘッダーの送信元アドレスとして、ネットワーク アダプターの現在の MAC アドレスを使用してください。                                                                                                                                                 |

 

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

 

 




