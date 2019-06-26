---
title: OID_GEN_UNKNOWN_PROTOS
description: クエリとしては、ネットワーク インターフェイス (RFC 2863 から ifInUnknownProtos) の不明なプロトコル パケット数を決定するのに OID_GEN_UNKNOWN_PROTOS OID を使用します。
ms.assetid: a0bebd8d-c202-41f5-84be-a3056a2eeef9
ms.date: 08/08/2017
keywords: -OID_GEN_UNKNOWN_PROTOS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3554cbcac043d374c4f945f3907eea5f255f1c16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385741"
---
# <a name="oidgenunknownprotos"></a>OID\_GEN\_不明な\_PROTOS


クエリとして、OID を使用して、\_GEN\_不明な\_ネットワーク インターフェイスの不明なプロトコル パケット数を決定する PROTOS OID (*ifInUnknownProtos*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

不明なプロトコルの統計情報のカウンターでは、関連付けられているプロトコルが不明であるかサポートされていないために破棄されたインターフェイスを介して受信したパケットの数を指定します。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、パケットの数を示す ULONG64 値。

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


[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




