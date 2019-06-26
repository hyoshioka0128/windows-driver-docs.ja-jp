---
title: NDIS_STATUS_WWAN_SMS_CONFIGURATION
description: ミニポート ドライバーは、前の OID_WWAN_SMS_CONFIGURATION の入力候補 MB サービスに通知する NDIS_STATUS_WWAN_SMS_CONFIGURATION 通知を使用して \ 160; クエリまたはセットの要求、または SMS の変更の場合、イベント通知構成します。 ミニポート ドライバーには、この通知が不要なイベントを送信できます。この通知は、NDIS_WWAN_SMS_CONFIGURATION 構造体を使用します。
ms.assetid: 86dfe2dc-070b-43d9-b6fa-54dee985c65d
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_CONFIGURATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bb3f97a1dcad87fb73eadfcb4a88c1dfa6b9d48f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386857"
---
# <a name="ndisstatuswwansmsconfiguration"></a>NDIS\_状態\_WWAN\_SMS\_構成


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスに、前のいずれかの完了に関する通知の構成通知[OID\_WWAN\_SMS\_構成](oid-wwan-sms-configuration.md) の照会または SMS 構成では、要求、または変更の場合、イベント通知を設定します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは、MB デバイスの SMS サブシステムが SMS 操作の準備ができたときこの迷惑なを示す値を送信する必要があります。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_SMS\_構成](oid-wwan-sms-configuration.md)

[**NDIS\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)

 

 




