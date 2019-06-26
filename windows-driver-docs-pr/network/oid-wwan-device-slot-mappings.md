---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO を設定または MB デバイス (つまり、executor スロット マッピング) のデバイスのスロットのマッピングを返します。
ms.assetid: 54AF3447-7918-49CE-945A-DC8DC1E78CBF
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 31294f80732f686d84ca212f31865e9b1458dc10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358599"
---
# <a name="oidwwandeviceslotmappinginfo"></a>OID\_WWAN\_デバイス\_スロット\_マッピング\_情報


OID\_WWAN\_デバイス\_スロット\_マッピング\_情報が (つまり、executor スロット マッピング) MB デバイスのデバイスのスロットのマッピングを取得または設定します。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info) executor、スロットのマッピングに関する情報を提供する構造体。

次の図は、クエリ要求を示しています。

![スロットのマッピングのクエリ](images/multi-SIM_8_slotMappingQuery.png)

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)を格納する構造体、 [ **WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_slot_mapping_info)構造体を現在のマッピングの状態を示します。 これは、セットの要求が失敗した場合でもは、true を保持します。 OID のセット要求、構造体の\_WWAN\_デバイス\_スロット\_マッピング\_情報[ **NDIS\_WWAN\_設定\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)します。

次の図は、セットの要求を示しています。

![スロットのマッピングの設定](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>注釈
-------

ホストは、最初の起動時に、モデム必要があるスロットと executor の既定のマッピングが必要です。 ホストは OID. 1.3 で設定操作を実行します\_WWAN\_デバイス\_スロット\_マッピング\_各 executor にバインドされているスロットを定義する情報。 ホストが再起動し、削除/挿入の間でマッピングを維持するために、モデムが必要です。 この OID は、executor 固有ではないと、デバイス上の任意の NDIS インスタンスに送信できます。 現在のマッピングは、上記のようにもクエリー可能性があります。

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
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

[**NDIS\_WWAN\_設定\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)

 

 




