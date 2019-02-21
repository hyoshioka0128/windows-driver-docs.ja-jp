---
title: OID_GEN_MEDIA_CONNECT_STATUS
description: クエリとしては、OID_GEN_MEDIA_CONNECT_STATUS OID は、ネットワーク上の NIC の接続の状態を要求します。
ms.assetid: 3ed26e62-a285-4b78-91c6-7c3cc0963570
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_CONNECT_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 72575278de3943b532989997a37fd8f3e8afcfa3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552955"
---
# <a name="oidgenmediaconnectstatus"></a>OID\_GEN\_メディア\_CONNECT\_状態


クエリ、OID として\_GEN\_メディア\_CONNECT\_状態 OID は、ネットワーク上の NIC の接続の状態を要求します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID を処理します。

OID\_GEN\_メディア\_CONNECT\_状態 OID は、次のシステム定義の値の 1 つとして、ネットワーク上の NIC の接続の状態を要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

呼び出す必要がありますもミニポート ドライバーでは、ネットワーク接続が失われたことを検知、ときに、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)または[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562) NDIS で関数を\_状態\_メディア\_(NDIS 5.1) の切断または NDIS\_状態\_リンク\_を持つ状態**MediaConnectStateDisconnected** MediaConnectState プロパティ (NDIS の 6.x)。 呼び出す必要がありますし、接続が復元されると、 **NdisM (Co) IndicateStatus** NDIS に\_状態\_メディア\_(NDIS 5.1) の接続または NDIS\_状態\_リンク\_を持つ状態**MediaConnectStateConnected** MediaConnectState プロパティ (NDIS の 6.x)。

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


[**NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




