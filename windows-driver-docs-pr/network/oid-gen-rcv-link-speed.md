---
title: OID_GEN_RCV_LINK_SPEED
description: クエリとして OID_GEN_RCV_LINK_SPEED OID を使用して、ネットワーク インターフェイスの受信リンク速度を決定します。 バージョン情報の Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: d66bdba3-93f4-4a5a-a658-9b1a2e1b9407
ms.date: 08/08/2017
keywords: -OID_GEN_RCV_LINK_SPEED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6bdc323af156d23a56013c80c23ab5f9c2099886
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386218"
---
# <a name="oidgenrcvlinkspeed"></a>OID\_GEN\_受信\_リンク\_速度


クエリとして、OID を使用して、\_GEN\_受信\_リンク\_ネットワーク インターフェイスの受信リンク速度を決定する速度の OID。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

インターフェイス プロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、受信を示す ULONG64 値の 1 秒あたりのビット単位で、インターフェイス リンク速度。

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


[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




