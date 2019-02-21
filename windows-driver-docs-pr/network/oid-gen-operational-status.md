---
title: OID_GEN_OPERATIONAL_STATUS
description: クエリとして OID_GEN_OPERATIONAL_STATUS OID を使用して、ネットワーク インターフェイス (RFC 2863 から ifOperStatus) の現在の運用状態を確認します。
ms.assetid: fa00d449-6ec0-4e72-8d9c-a453a0b1f3e9
ms.date: 08/08/2017
keywords: -OID_GEN_OPERATIONAL_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 13905453dcb5f8bc420d44cb7cd8cdf004535161
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531238"
---
# <a name="oidgenoperationalstatus"></a>OID\_GEN\_OPERATIONAL\_状態


クエリとして、OID を使用して、\_GEN\_運用\_ネットワーク インターフェイスの現在の運用状態を確認する状態の OID (*ifOperStatus*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

NDIS ミニポート アダプターとフィルター モジュールでは、この OID の処理とのみ[NDIS ネットワーク インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダーがこの OID クエリを受信します。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、値のいずれかで指定できます、 [ **NET\_場合\_工程\_ステータス**](https://msdn.microsoft.com/library/windows/hardware/ff568746)列挙体。

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


[**NET\_場合\_工程\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff568746)

[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




