---
title: OID_GEN_ALIAS
description: クエリとして OID_GEN_ALIAS OID を使用して、(RFC 2863 から ifAlias) インターフェイスのエイリアスの文字列を取得します。 バージョン情報の Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: ff5e6494-aa4e-4a0a-b773-64b612236c8c
ms.date: 08/08/2017
keywords: -OID_GEN_ALIAS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 361c0dfc20777c407824a41c82b062a0f1ea718c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385501"
---
# <a name="oidgenalias"></a>OID\_GEN\_エイリアス


クエリとして、OID を使用して、\_GEN\_インターフェイスのエイリアスの文字列を取得するエイリアスの OID (*ifAlias*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーは、そのインターフェイスの一意のエイリアス文字列を割り当てることができます。 名前は、同じインターフェイスと関連付けられたままする必要があります、プロバイダーは、コンピューターの再起動後に永続的な文字列と reinitializations にことができます。

NDIS ネットワーク インターフェイスのプロバイダーとそのためミニポート ドライバーではありませんサポートまたはだけフィルター ドライバー、する必要がありますこの OID OID 要求として。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、NDIS で返されるエイリアス文字列\_場合\_カウント済\_文字列構造体。

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

 

 




