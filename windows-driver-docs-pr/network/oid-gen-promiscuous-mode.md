---
title: OID_GEN_PROMISCUOUS_MODE
description: クエリとして、ネットワーク インターフェイスが無作為検出しているかどうかを判断する OID_GEN_PROMISCUOUS_MODE OID を使用します (RFC 2863 から ifPromiscuousMode)。
ms.assetid: c3ba0908-724c-4149-a66f-5c3d41751165
ms.date: 08/08/2017
keywords: -OID_GEN_PROMISCUOUS_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4278589603de9763b31e1d2f5365cfd8936ddeaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552947"
---
# <a name="oidgenpromiscuousmode"></a>OID\_GEN\_PROMISCUOUS\_モード


クエリとして、OID を使用して、\_GEN\_PROMISCUOUS\_ネットワーク インターフェイスが無作為検出しているかどうかを判断するモードの OID (*ifPromiscuousMode*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功インターフェイスがそのインターフェイスに送られるパケットのみを受け入れる場合、結果の値を指定する必要があります**FALSE**します。 この値は**TRUE**インターフェイスがすべてのネットワーク パケットを受け入れる場合。

<a name="requirements"></a>要件
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


[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




