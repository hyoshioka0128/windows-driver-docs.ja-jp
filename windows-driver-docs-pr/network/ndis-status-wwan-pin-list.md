---
title: NDIS_STATUS_WWAN_PIN_LIST
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PIN_LIST 通知を使用して OID_WWAN_PIN_LIST の OID クエリ要求に応答します。 ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。この通知では、NDIS_WWAN_PIN_LIST 構造体が使用されます。
ms.assetid: fd8e6734-d032-445a-819a-0d5a773e9ea3
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_PIN_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 0a27a714d3dbee5c630b683f8fe3f66d9025d03a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844701"
---
# <a name="ndis_status_wwan_pin_list"></a>NDIS\_ステータス\_WWAN\_PIN\_一覧


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_PIN\_リスト通知を使用して、 [oid\_](oid-wwan-pin-list.md)の oid クエリ要求に応答します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_PIN\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)構造を使用します。

<a name="remarks"></a>注釈
-------

これは、OID\_WWAN\_PIN\_リストの OID クエリ要求への応答のみを示す通知です。 この表示には、要求されていない表示は想定されていません。

OID\_WWAN\_PIN の有効化または無効化操作の結果として PIN 入力モードが変更されても、\_は、NDIS のステータス\_WWAN\_PIN\_一覧表示されません。

デバイスでサポートされているすべてのピンの現在の PinMode は、各クエリ要求のミニポートドライバーによって現在の状態を反映するように更新する必要があることに注意してください。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_PIN\_リスト](oid-wwan-pin-list.md)

[**NDIS\_WWAN\_PIN\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

 

 




