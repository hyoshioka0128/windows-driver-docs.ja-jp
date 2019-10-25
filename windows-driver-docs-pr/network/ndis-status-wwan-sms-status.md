---
title: NDIS_STATUS_WWAN_SMS_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SMS_STATUS 通知を使用して mb サービスに、MB デバイスのメッセージストアがいっぱいになったことを通知します。新しい SMS テキストメッセージが到着しました。 MessageIndex に対応する新しいメッセージが表示されます。ミニポートドライバーは、この通知を使用して、要請されていないイベントを送信することもできます。この通知では、NDIS_WWAN_SMS_STATUS 構造体が使用されます。
ms.assetid: 65553a3f-57af-49ef-a3b7-ed35df0a319d
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SMS_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ce00553a17a3398f2f3ff20a43a967860039fcd3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844629"
---
# <a name="ndis_status_wwan_sms_status"></a>NDIS\_ステータス\_WWAN\_SMS\_の状態


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SMS\_状態通知を使用して、MB サービスに次のイベントについて通知します。

-   MB デバイスのメッセージストアがいっぱいです。

-   新しい SMS テキストメッセージが到着しました。 *Messageindex*に対応する新しいメッセージが表示されます。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_SMS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)構造を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SMS\_ステータスを使用して、すべての非クラス 0 (フラッシュ/アラート) メッセージの到着を MB サービスに通知する必要があります。 クラス-0 (フラッシュ/アラート) メッセージの到着に関する情報を MB サービスに通知するには、ミニポートドライバーで、 [**SMS\_受信\_の NDIS\_ステータス\_WWAN**](ndis-status-wwan-sms-receive.md)を使用する必要があります。

これは、OID\_WWAN\_SMS\_の状態または要請されていないイベントの*クエリ*要求に対するトランザクション通知である可能性があります。

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


[**NDIS\_WWAN\_SMS\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)

[**NDIS\_ステータス\_WWAN\_SMS\_受信**](ndis-status-wwan-sms-receive.md)

 

 




