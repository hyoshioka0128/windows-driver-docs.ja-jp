---
title: NDIS_STATUS_WWAN_READY_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_READY_INFO 通知を使用して、OID_WWAN_READY_INFO \ 160; クエリ要求に応じて、デバイスの準備完了状態の変更を MB サービスに通知します。
ms.assetid: 92ddf95f-8829-4259-b53a-c7ce56ee53f0
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_READY_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a8ac58f7e0c8680c9ec0a9fe6c34b30a15c503b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844651"
---
# <a name="ndis_status_wwan_ready_info"></a>NDIS\_ステータス\_WWAN\_準備完了\_情報


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_READY\_情報通知を使用して、 [OID\_WWAN\_準備完了\_情報](oid-wwan-ready-info.md) クエリ要求に応答して、デバイスの準備完了状態の変更を MB サービスに通知します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_READY\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)構造体を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、デバイスの準備が完了しているすべての変更を一方的なイベントとして報告する必要があります。 ミニポートドライバーが MB デバイスを初期化すると、ミニポートドライバーは、WWAN\_READY\_INFO **ReadyState**メンバーを**WwanReadyStateOff**に設定する必要があります。 その後、ミニポートドライバーは、この通知を使用して、デバイスの準備完了状態の変更を MB サービスに報告する必要があります。 たとえば、ミニポートドライバーは、 **ReadyState**メンバーが**WwanReadyStateOff**から**WwanReadyStateDeviceLocked**または**WwanReadyStateBadSim** **に変更された場合に、デバイスの準備完了状態の変更を報告する必要があります。WwanReadyStateSimNotInserted**、またはその他のさまざまなデバイスの準備完了状態。

デバイスの準備が完了しているほとんどの変更は、デバイスがラジオスタックと SIM カードを初期化したときに発生します (必要な場合)。 また、MB サービスとミニポートドライバー (ユーザーが SIM カードを変更するなど) の間のセッション中にも、変更が発生する可能性があります。 MB サービスの動作は、新しいデバイスの準備完了状態に応じて変更されます。

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


[**NDIS\_WWAN\_準備完了\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)

[OID\_WWAN\_準備完了\_情報](oid-wwan-ready-info.md)

 

 




