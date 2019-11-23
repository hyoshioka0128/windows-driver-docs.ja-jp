---
title: NDIS_STATUS_WWAN_SMS_CONFIGURATION
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SMS_CONFIGURATION 通知を使用して、以前の OID_WWAN_SMS_CONFIGURATION \ 160、クエリまたは set 要求の完了、または SMS の変更の場合のイベント通知を MB サービスに通知します。configuration. ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。この通知では、NDIS_WWAN_SMS_CONFIGURATION 構造を使用します。
ms.assetid: 86dfe2dc-070b-43d9-b6fa-54dee985c65d
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_SMS_CONFIGURATION
ms.localizationpriority: medium
ms.openlocfilehash: e017232daa44e5c6f772dfec8394b8e9684e5fbe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844637"
---
# <a name="ndis_status_wwan_sms_configuration"></a>NDIS\_ステータス\_WWAN\_SMS\_構成


ミニポートドライバーは、NDIS の\_ステータス\_WWAN\_SMS\_構成通知を使用して、以前の[OID\_wwan\_configuration](oid-wwan-sms-configuration.md)\_のクエリまたは set 要求の完了、または sms 構成の変更の場合のイベント通知のいずれかを MB サービスに通知します。 

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)構造を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、MB デバイスの SMS サブシステムが SMS 操作の準備ができている場合に、この要請されていないという通知を送信する必要があります。

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


[OID\_WWAN\_SMS\_構成](oid-wwan-sms-configuration.md)

[**NDIS\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)

 

 




