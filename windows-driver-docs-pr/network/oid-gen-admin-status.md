---
title: OID_GEN_ADMIN_STATUS
description: クエリとしては、(RFC 2863 から ifAdminStatus) インターフェイスの管理の状態を確認するのに OID_GEN_ADMIN_STATUS OID を使用します。
ms.assetid: e8f45521-7419-4c11-b84b-36d4d3306fc2
ms.date: 08/08/2017
keywords: -OID_GEN_ADMIN_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 548b87f7b79538e3f77952fe16596b9a086d4153
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356145"
---
# <a name="oidgenadminstatus"></a>OID\_GEN\_管理者\_状態


クエリとして、OID を使用して、\_GEN\_管理者\_インターフェイス管理状態を確認する状態の OID (*ifAdminStatus*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

管理の状態は、システム管理者が要求した状態です。

のみ[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、値のいずれかで指定できます、 [ **NET\_場合\_管理者\_ステータス**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_admin_status)列挙体。

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


[**NET\_場合\_管理者\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_admin_status)

[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




