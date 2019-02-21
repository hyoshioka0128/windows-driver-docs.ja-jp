---
title: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE
description: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE は、EAPOL 要求の ID のメッセージのパターンの wake on LAN の ID を含む TLV です。
ms.assetid: CB898EF0-3ACF-4026-8650-91EF18E93766
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c001768bb778e609b33dfa8e5013da8b86f31a34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550640"
---
# <a name="wditlvwakepacketeapolrequestidmessage"></a>WDI\_TLV\_WAKE\_パケット\_EAPOL\_要求\_ID\_メッセージ


WDI\_TLV\_WAKE\_パケット\_EAPOL\_要求\_ID\_メッセージは、TLV EAPOL 要求の ID のメッセージのパターンの wake on LAN の ID を格納します。

## <a name="tlv-type"></a>TLV 型


0x5F

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                           |
|--------|---------------------------------------|
| UINT32 | Wake on LAN のパターンの ID を指定します |

 

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

 

 




