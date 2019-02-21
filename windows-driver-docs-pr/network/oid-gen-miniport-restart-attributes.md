---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID は、アダプターのミニポート再起動属性、NDIS ドライバー スタックの伝達の一般的な属性を識別します。
ms.assetid: 239993f6-2176-4925-aadc-44e0df66f56b
ms.date: 08/08/2017
keywords: -OID_GEN_MINIPORT_RESTART_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2cb128805f2e0c682bfda9307d64cf357d77efcf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528470"
---
# <a name="oidgenminiportrestartattributes"></a>OID\_GEN\_ミニポート\_再起動\_属性


OID\_GEN\_ミニポート\_再起動\_属性 OID、NDIS ドライバー スタックのミニポート アダプター再起動属性の伝達の一般的な属性を識別します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a name="remarks"></a>注釈
-------

OID\_GEN\_ミニポート\_再起動\_属性 OID は OID クエリを発行するか、要求の設定は使用されません。

場合、 **Oid**内のメンバー、 [ **NDIS\_再起動\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)構造体は OID\_GEN\_ミニポート\_再起動\_属性、**データ**、構造体のメンバーが含まれています、 [ **NDIS\_再起動\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567260)構造体。

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


[**NDIS\_再起動\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)

[**NDIS\_再起動\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567260)

 

 




