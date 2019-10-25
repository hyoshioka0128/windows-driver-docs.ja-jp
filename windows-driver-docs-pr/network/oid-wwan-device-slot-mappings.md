---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO は、MB デバイス (つまり、実行プログラムとスロットのマッピング) のデバイススロットのマッピングを設定または返します。
ms.assetid: 54AF3447-7918-49CE-945A-DC8DC1E78CBF
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: bc74598b3b69f9d27d3fe304b4117ea350f98051
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843854"
---
# <a name="oid_wwan_device_slot_mapping_info"></a>OID\_WWAN\_デバイス\_スロット\_マッピング\_情報


OID\_WWAN\_デバイス\_スロットは\_情報をマップ\_します。または、MB デバイス (実行プログラム-スロットのマッピング) のデバイススロットのマッピングを返します。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_状態\_を返してから、後で[**ndis\_ステータス\_WWAN\_デバイスを送信する前に、元の要求に必要な\_を返します。8_ スロット\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings) 、 [**NDIS\_WWAN\_デバイス\_スロット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)を含む\_情報ステータス通知をマップします。\_INFO 構造をマッピングして、実行プログラムとスロット間のマッピングに関する情報を提供します。

次の図は、クエリ要求を示しています。

![スロットマッピングクエリ](images/multi-SIM_8_slotMappingQuery.png)

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_ステータス\_を返してから、後で[**ndis\_ステータス\_WWAN\_デバイスを送信する前に、元の要求に必要な\_を返し\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)の状態通知。 [**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)構造に含まれています。これには、さらに wwan\_デバイスが含まれて[ **\_スロット\_\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_slot_mapping_info)構造をマッピングして現在のマッピング状態を示します。 これは、set 要求が失敗した場合でも当てはまります。 OID\_\_デバイス\_スロットに対する set 要求の構造は\_情報\_マッピング\_[**デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)\_\_\_の\_情報のマッピング\_ます。

次の図は、セット要求を示しています。

![スロットマッピングセット](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>注釈
-------

ホストは、最初の起動時に、モデムにスロットとエグゼキュータの間に既定のマッピングが設定されていることを前提としています。 ホストは、OID\_WWAN\_デバイス\_スロットを使用して設定操作を実行し\_\_情報をマップして、各実行プログラムにバインドされているスロットを定義します。 ホストは、再起動と削除/挿入の間にマッピングを維持するようにモデムに要求します。 この OID は実行プログラム固有ではなく、デバイス上の任意の NDIS インスタンスに送信される場合があります。 また、上記のように現在のマッピングに対してクエリを実行することもできます。

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


[**NDIS\_ステータス\_WWAN\_デバイス\_スロット\_\_情報のマッピング**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

[**NDIS\_WWAN\_\_デバイス\_スロットの設定\_情報のマッピング\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)

 

 




