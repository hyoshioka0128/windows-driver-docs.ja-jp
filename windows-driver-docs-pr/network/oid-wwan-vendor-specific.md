---
title: OID_WWAN_VENDOR_SPECIFIC
description: OID_WWAN_VENDOR_SPECIFIC では、ベンダー固有のオブジェクトを実装するミニポート ドライバーを許可します。
ms.assetid: 7c1843bc-3d60-437c-a24d-6da82262a468
ms.date: 08/08/2017
keywords: -OID_WWAN_VENDOR_SPECIFIC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4a647fe74b14f5ca8c7ddaed8156046c0c7d4d31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384233"
---
# <a name="oidwwanvendorspecific"></a>OID\_WWAN\_ベンダー\_特定


OID\_WWAN\_ベンダー\_により、特定のベンダー固有のオブジェクトを実装するために、ミニポート ドライバー。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_ベンダー\_特定**](ndis-status-wwan-vendor-specific.md)ベンダー定義の構造体を格納している状態通知が完了しているときに、プライベート オブジェクトを実装するために、トランザクションです。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN 仕入先の特定の操作](https://msdn.microsoft.com/library/windows/hardware/ff559138)します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_ベンダー固有の操作をサポートしていない場合にサポートされています。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WWAN 仕入先の特定の操作](https://msdn.microsoft.com/library/windows/hardware/ff559138)

[**NDIS\_状態\_WWAN\_ベンダー\_特定**](ndis-status-wwan-vendor-specific.md)

 

 




