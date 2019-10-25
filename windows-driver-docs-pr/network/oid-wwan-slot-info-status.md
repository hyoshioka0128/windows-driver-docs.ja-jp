---
title: OID_WWAN_SLOT_INFO
description: OID_WWAN_SLOT_INFO は、指定された UICC スロットとその中のカード (存在する場合) の高レベルの集計された状態を取得します。 また、いずれかのスロットの状態が変化したときに、要請されていない通知を配信するためにも使用できます。
ms.assetid: 6267D480-5055-4A7A-B2A0-F4DF9154DCD7
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SLOT_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5d6d360c02668fd352ca0847287fb254b1291a31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843789"
---
# <a name="oid_wwan_slot_info"></a>OID\_WWAN\_スロット\_情報


OID\_WWAN\_スロット\_情報は、指定された UICC スロットとその中のカード (存在する場合) の高レベルの集計された状態を取得します。 また、いずれかのスロットの状態が変化したときに、要請されていない通知を配信するためにも使用できます。

ミニポートドライバーは、クエリ要求を非同期的に処理する必要があります。最初に NDIS\_STATUS\_を返してから、後で[**ndis\_ステータス\_WWAN\_スロットを送信する前に、元の要求に必要な\_を示し\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status) [**NDIS\_WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)構造を含む情報ステータス通知。この構造体には、 [**WWAN\_スロット\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)構造体が含まれており、これにより、モデムシステム全体に関する情報が提供されます。機能.

クエリ要求では、 [**NDIS\_WWAN\_入力として\_スロット\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)構造を取得します。 ミニポートドライバーは、WWAN の**SlotIndex**メンバーに指定されているスロット ID に従って、スロットの状態を返す必要があります[ **\_スロット\_INFO 構造体\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)します。

次の図は、クエリ要求を示しています。

![スロットの状態のクエリ](images/multi-SIM_9_slotStatusQuery.png)

Set 要求は適用できません。

Ndis [ **\_ステータス\_wwan\_スロットの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)通知は、 [**ndis\_WWAN\_スロット\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)構造を使用して、スロット/カードの状態が変化したときにホストに送信されます。

<a name="remarks"></a>注釈
-------

ホストは、OID\_WWAN\_スロット\_情報を使用して、モデムの特定のスロットの状態を照会します。 この OID は実行プログラム固有ではなく、1つのモデムに属する任意の NDIS インスタンスに送信できます。 スロットの状態は、スロットとカードの両方の状態の概要を表します。

報告される状態のセットは、スロットハードウェアの機能によって制限されます。 最も制限の厳しいケースでは、スロットハードウェアでは、電源が入ってアクティブになったときにカードが存在することだけを判断できます。このような場合、 **Offempty**と**Off**の状態は報告されません。

[Oid\_wwan\_準備ができている\_情報](oid-wwan-ready-info.md)と OID\_WWAN\_スロット\_情報。デバイスの準備ができている SIM カードスロットの状態を取得するのと同じコア機能を実行します。ただし、OID\_WWAN\_READY\_INFO は実行プログラムごとのコマンドですが、OID\_WWAN\_スロット\_INFO は任意の物理インスタンス (実行プログラム) で使用できます。また、この情報がない場合でも、適切なスロットの状態を返すことが想定されています。現時点では、任意のエグゼキュータにマップされます。

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
<td><p>Windows 10 バージョン1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ステータス\_WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)

[**NDIS\_WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

[**WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)

[**NDIS\_WWAN\_\_スロット\_情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)

[**WWAN\_\_スロット\_情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)

[**WWAN\_UICCSLOT\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_uiccslot_state)

[OID\_WWAN\_準備完了\_情報](oid-wwan-ready-info.md)

 

 




