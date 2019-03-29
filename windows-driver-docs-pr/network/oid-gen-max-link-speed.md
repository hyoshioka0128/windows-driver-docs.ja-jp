---
title: OID_GEN_MAX_LINK_SPEED
description: クエリとして NDIS および上にあるドライバーを使用して OID_GEN_MAX_LINK_SPEED OID 最大送信をサポートおよびミニポート アダプターのリンク速度を受信します。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -OID_GEN_MAX_LINK_SPEED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bbfdbdb9d0dd747be6e650d2298e4aafa4f4d67b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579507"
---
# <a name="oidgenmaxlinkspeed"></a>OID\_GEN\_最大\_リンク\_速度


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_最大\_リンク\_ミニポート アダプターのリンク速度の送受信をサポートされている最大を決定する速度の OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>コメント
-------

ミニポート ドライバーでは、初期化中に最大リンク速度を提供します。

最大のリンク速度を指定するには、設定、 **MaxXmitLinkSpeed**と**MaxRcvLinkSpeed**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。 ミニポート ドライバーがこの OID をサポートしていない場合、ドライバーは NDIS を返す必要があります\_状態\_いない\_サポートされています。 ミニポート ドライバーでは、この OID をサポートする場合の最大数のリンク速度が返されます、 [ **NDIS\_リンク\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_リンク\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

 

 




