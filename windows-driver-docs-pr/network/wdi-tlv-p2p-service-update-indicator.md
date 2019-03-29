---
title: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR
description: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR は、Wi-Fi Direct サービスを含む TLV は、インジケーターを更新します。
ms.assetid: C90579C9-55DD-4E32-BEA3-EB156F4A422C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 92ef75f7cf9906580a275229b12f60be30f7113d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574999"
---
# <a name="wditlvp2pserviceupdateindicator"></a>WDI\_TLV\_P2P\_サービス\_UPDATE\_インジケーター


WDI\_TLV\_P2P\_サービス\_更新\_インジケーターが Wi-Fi Direct サービスの更新のインジケーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x115

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | サービス情報の検出 ANQP 要求に応答して、ドライバーがサポートしている場合、ANQP 応答に含めるサービス更新プログラムのインジケーター。 |

 

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

 

 




