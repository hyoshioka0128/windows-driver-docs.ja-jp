---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状態では、ドライバーの後続パケット フィルターの変更を示します。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PACKET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f5d9922ba3eab75edcfab51dcc1ac9203987b45d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386221"
---
# <a name="ndisstatuspacketfilter"></a>NDIS\_状態\_パケット\_フィルター


NDIS\_状態\_パケット\_フィルター状態は、ドライバーの後続パケット フィルター変更を示します。 NDIS は、ミニポート アダプターのパケット フィルターの設定の変更が存在する可能性を上にあるドライバーに通知するミニポート アダプターの場合は、この状態インジケーターを生成します。

<a name="remarks"></a>注釈
-------

NDIS は NDIS は、NDIS を生成するときに、パケット フィルターが変更されたことを保証していない\_状態\_パケット\_フィルター状態を示す値。

NDIS フィルター ドライバーでは、NDIS を生成できますも\_状態\_パケット\_フィルター状態を示す値。

NDIS フィルター型フラグのビットごとの OR を提供する、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 フィルターの型のフラグの一覧は、次を参照してください。、 [OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575) OID。 パケット フィルターの詳細については、次を参照してください。 [OID\_GEN\_サポートされている\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569643)します。

**StatusBufferSize**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373) sizeof(ULONG) に構造体が設定されています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)

[OID\_GEN\_サポートされている\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569643)

 

 




