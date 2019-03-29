---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC では、新しい NDIS ポートを作成するミニポート ドライバーを要求します。
ms.assetid: 4EF98858-86CD-409B-BE41-E57B24158609
ms.date: 08/08/2017
keywords: -OID_WWAN_CREATE_MAC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0d1a9d416aa8890ca81aa0dd9ae54d3183bd5aad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578639"
---
# <a name="oidwwancreatemac"></a>OID\_WWAN\_作成\_MAC


OID\_WWAN\_作成\_MAC は、新しい NDIS ポートを作成するミニポート ドライバーを要求します。 追加の PDP コンテキストのコンテキストのアクティブ化要求は、この新しい NDIS ポートで送信されます。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求と後で使用して要求を完了するには、必要な作業、 [ **NDIS\_WWAN\_MAC\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn449747)ポートに関連付けられているポート番号の NDIS と MAC アドレスを示す構造体。

クエリ要求はサポートされていません。

<a name="remarks"></a>コメント
-------

ミニポート ドライバーを作成する要求を処理する必要があります (アクティブ化) のデッドロックを防ぐために非同期的に新しい NDIS ポート。

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
<td><p>Windows 8.1 と Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_MAC\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn449747)

[OID\_WWAN\_削除\_MAC](oid-wwan-delete-mac.md)

 

 




