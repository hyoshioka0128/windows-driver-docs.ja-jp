---
title: NDIS_STATUS_WWAN_RADIO_STATE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_RADIO_STATE 通知を使用して、ユーザーがハードウェアの無線電源を変更したときに MB サービスに通知します。または、OID クエリまたは set 要求の OID_WWAN_RADIO_ に応じて、デバイスのソフトウェアベースの無線電源状態の変更を通知します。状態. ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。この通知では、NDIS_WWAN_RADIO_STATE 構造体が使用されます。
ms.assetid: 77c10b2a-ab43-4349-947a-e89c7af27f68
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_RADIO_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: afc337a817bf93a64eaafea614f4cc9584c8e173
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844717"
---
# <a name="ndis_status_wwan_radio_state"></a>NDIS\_ステータス\_WWAN\_ラジオ\_状態


ミニポートドライバーは、ユーザーがハードウェアの無線電源を変更したとき、または OID クエリに応答してデバイスのソフトウェアベースの無線電源状態の変化を通知するために、NDIS\_ステータス\_WWAN\_ラジオ\_状態通知を使用します。または、 [OID\_WWAN\_無線\_状態](oid-wwan-radio-state.md)の要求を設定します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_RADIO\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)構造体を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、クエリ要求への応答として、現在のハードウェアベースおよびソフトウェアベースの無線電源状態の両方を返す必要があります。

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


[**NDIS\_WWAN\_無線\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[OID\_WWAN\_無線\_の状態](oid-wwan-radio-state.md)

 

 




