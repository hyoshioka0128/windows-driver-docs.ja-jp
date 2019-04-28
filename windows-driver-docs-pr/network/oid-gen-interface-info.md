---
title: OID_GEN_INTERFACE_INFO
description: クエリとして OID_GEN_INTERFACE_INFO OID を使用して、ネットワーク インターフェイスの現在の状態と統計情報を取得します。
ms.assetid: fa1dd52f-7cf6-4e95-af15-02ae65fcb872
ms.date: 08/08/2017
keywords: -OID_GEN_INTERFACE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3a094db6a5c26df79dac06e9fcf879ec2d9a33da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375679"
---
# <a name="oidgeninterfaceinfo"></a>OID\_GEN\_インターフェイス\_情報


クエリとして、OID を使用して、\_GEN\_インターフェイス\_ネットワーク インターフェイスの現在の状態と統計情報を取得する情報の OID。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、 [ **NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)構造体。 この構造体には、インターフェイスの有効期間中に変化する情報が含まれています。

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


[**NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




