---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: セットとして NDIS および上にあるドライバーは、NDIS ポートの現在の状態を設定するのに OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID を使用します。
ms.assetid: 676601c1-2647-4341-9a5c-cee895d2dbf7
ms.date: 08/08/2017
keywords: -OID_GEN_PORT_AUTHENTICATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9b2230aee48474c366ff83bceec56be8b535b084
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380861"
---
# <a name="oidgenportauthenticationparameters"></a>OID\_GEN\_ポート\_認証\_パラメーター


セットとして NDIS と関連付けたドライバー使用 OID\_GEN\_ポート\_認証\_NDIS ポートの現在の状態を設定するパラメーターの OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。 NDIS ポートは必須です。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

ミニポート ドライバーがこの OID をサポートしていない場合、ミニポート ドライバーが NDIS を返す必要があります\_状態\_いない\_サポートされています。

ミニポート ドライバーでは、この OID をサポートする場合、ドライバーは返します NDIS\_状態\_成功には、受信ポートの方向、ポート コントロールの状態、および認証の状態、 [ **NDIS\_ポート\_認証\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)構造体。

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


[**NDIS\_ポート\_認証\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)

 

 




