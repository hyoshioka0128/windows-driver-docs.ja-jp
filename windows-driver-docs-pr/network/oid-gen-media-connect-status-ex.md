---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: クエリとしては、OID_GEN_MEDIA_CONNECT_STATUS_EX OID は、インターフェイスの接続の状態を返します。 Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_CONNECT_STATUS_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 340d83dee8f23949dd80e88e398dd92ee1a721cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580446"
---
# <a name="oidgenmediaconnectstatusex"></a>OID\_GEN\_メディア\_CONNECT\_状態\_例


クエリ、OID として\_GEN\_メディア\_CONNECT\_状態\_EX OID がインターフェイスの接続状態を返します。

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>コメント
-------

NDIS の接続の状態を照会するこの OID を使用して、[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダー。 のみ NDIS インターフェイス プロバイダー、およびしたがってミニポート ドライバーではないまたはフィルター ドライバー、する必要がありますサポートこの OID OID 要求として。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、値のいずれかで指定できます、 [ **NET\_場合\_メディア\_CONNECT\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff568744)列挙体。

ミニポート ドライバー供給メディアは、初期化中に状態を接続し、状態インジケーターの更新プログラムを提供します。

ミニポート ドライバーで接続状態を指定するには、設定、 **MediaConnectState**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

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


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[**NET\_場合\_メディア\_CONNECT\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff568744)

[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




