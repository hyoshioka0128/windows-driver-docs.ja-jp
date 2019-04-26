---
title: OID_PNP_QUERY_POWER
description: OID_PNP_QUERY_POWER
ms.assetid: 62675042-3339-48de-97bb-58bfa05e1b39
ms.date: 08/08/2017
keywords: -OID_PNP_QUERY_POWER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 95612f7679bc453462154b3f99de3ee022cbda64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351718"
---
# <a name="oidpnpquerypower"></a>OID\_PNP\_クエリ\_電源





OID\_PNP\_クエリ\_POWER OID 要求をそのネットワーク アダプターに指定された低電力状態を遷移できるかどうかを示すために、ミニポート ドライバー、 *InformationBuffer*します。 低電力状態が NDIS が次のいずれかとして指定された\_デバイス\_POWER\_状態の値。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
これには、D1 のデバイスの状態を指定します。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
これには、D2 のデバイスの状態を指定します。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
これには、D3 のデバイスの状態を指定します。

OID\_PNP\_クエリ\_D0 のデバイスの状態への遷移を要求するのには電源要求は使用されません。 NDIS は単純に送信します、 [OID\_PNP\_設定\_POWER](oid-pnp-set-power.md) D0 のデバイスの状態を指定する要求。

NDIS を返すことによって\_状態\_この oid の成功を要求、ミニポート ドライバーでは、ネットワーク アダプターに後続の OID の受信時に指定したデバイスの電源状態に変わりますが保証されます\_PNP\_設定\_POWER 要求。 ミニポート ドライバーでは、ここでは、する必要があります何もしない移行を危険にさらし。

ミニポート ドライバーは、NDIS を返す必要があります常に\_状態\_この OID 要求に成功します。 他のリターン コードは、エラーです。

OID\_PNP\_クエリ\_POWER 要求が常に続く OID\_PNP\_設定\_POWER 要求。 OID\_PNP\_設定\_POWER 要求に OID 続けて\_PNP\_クエリ\_電源を要求または未指定の間隔、oid 後くる可能性があります\_PNP\_クエリ\_POWER 要求。 D0 OID で指定されたデバイスの状態\_PNP\_設定\_POWER 要求が、OID を効果的にキャンセル\_PNP\_クエリ\_POWER 要求。

中間のドライバーは、NDIS を返す必要があります常に\_状態\_OID のクエリに成功\_PNP\_クエリ\_電源。 中間のドライバーは、OID を伝達することはありません\_PNP\_クエリ\_電源要求の基になる、ミニポート ドライバーにします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 5.1、および NDIS 6.0 以降がサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




