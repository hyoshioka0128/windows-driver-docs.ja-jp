---
title: OID_GEN_RNDIS_CONFIG_PARAMETER
description: セットとして、OID_GEN_RNDIS_CONFIG_PARAMETER はデバイス固有のパラメーターを設定するのに使用されます。
ms.assetid: 79e74e8b-7811-46a5-8ede-f6cca92967b0
ms.date: 08/08/2017
keywords: -OID_GEN_RNDIS_CONFIG_PARAMETER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 71c28e88e08d7f937cf675a8f1dbc176372eb549
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355119"
---
# <a name="oidgenrndisconfigparameter"></a>OID\_GEN\_RNDIS\_CONFIG\_パラメーター


OID、セットとして\_GEN\_RNDIS\_CONFIG\_デバイス固有のパラメーターを設定するパラメーターを使用します。 ホストは、RNDIS デバイスのみで使用します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 RNDIS デバイスでのみ使用します。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a name="remarks"></a>コメント
-------

OID\_GEN\_RNDIS\_CONFIG\_RNDIS デバイスとパラメーターを使用します。 デバイス固有のパラメーターを設定するのにホストを使用します。 ミニポート ドライバーでは使用されません。 この OID の詳細については、次を参照してください。[デバイスに固有のパラメーターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-device-specific-parameters)します。

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

 

 




