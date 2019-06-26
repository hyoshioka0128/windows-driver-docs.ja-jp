---
title: NDIS_STATUS_MEDIA_CONNECT
description: NDIS_STATUS_MEDIA_CONNECT 状態では、接続から切断されているデバイスのネットワーク接続の状態が変更されたことを示します。
ms.assetid: de03d265-c8bf-4b7d-bfff-f583fcf08904
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_MEDIA_CONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4bdc7fb6c0ff013105d9d1b2cc50cb3171706416
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383266"
---
# <a name="ndisstatusmediaconnect"></a>NDIS\_状態\_メディア\_接続


NDIS\_状態\_メディア\_CONNECT のステータスは、デバイスのネットワーク接続の状態が変更されたことから切断されたに接続されていることを示します。 たとえば、デバイスは、(ワイヤレス デバイス) のアクセス ポイントの範囲内で言えば、または、ユーザーがデバイスのネットワーク ケーブルを接続するときを接続します。

<a name="remarks"></a>注釈
-------

NDIS 変換 NDIS\_状態\_メディア\_への接続状態インジケーター [ **NDIS\_状態\_リンク\_状態**](ndis-status-link-state.md)NDIS 6.0 のドライバーを後続の状態のインジケーター。

NDIS 5。*x*以前のミニポート ドライバーを示し、 [ **NDIS\_状態\_メディア\_切断**](ndis-status-media-disconnect.md)ときミニポート ドライバーの状態ネットワーク接続が失われたことを決定します。 接続が復元されると、ドライバーは、NDIS を示します\_状態\_メディア\_CONNECT のステータス。

NDIS の詳細については\_状態\_メディア\_接続を参照してください[を示す接続の状態 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546856(v=vs.85))と[802.11 ネットワークのメディアの状態インジケーター](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549301(v=vs.85)).

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
<td><p>NDIS 6.0 以降はサポートされていません (を使用して、 <a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"> <strong>NDIS_STATUS_LINK_STATE</strong> </a>代わりに)。 Windows Vista および Windows XP で 5.1 の NDIS ドライバーのみサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_リンク\_状態**](ndis-status-link-state.md)

[**NDIS\_状態\_メディア\_切断**](ndis-status-media-disconnect.md)

 

 




