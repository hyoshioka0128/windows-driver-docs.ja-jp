---
title: NDIS_STATUS_WWAN_SMS_RECEIVE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SMS_RECEIVE 通知を使用して、OID_WWAN_SMS_READ \ 160; クエリ要求による前の読み取り要求の完了、またはからの新しいクラス-0 (フラッシュ/アラート) メッセージの到着を MB サービスに通知します。イベント通知としてのネットワークプロバイダー。 ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。この通知では、NDIS_WWAN_SMS_RECEIVE 構造体が使用されます。
ms.assetid: fc1c3587-8bba-4ffd-9561-4140c307c705
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SMS_RECEIVE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5bef42d6826fe96369f866fdcff38bcc6c9f2f6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844635"
---
# <a name="ndis_status_wwan_sms_receive"></a>NDIS\_ステータス\_WWAN\_SMS\_受信


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SMS\_を使用して、MB サービスに対して、 [OID\_wwan\_sms](oid-wwan-sms-read.md)\_の読み取りに関する前の読み取り要求の完了を通知し クエリ要求、またはネットワークプロバイダーからのイベント通知としての新しい class-0 (flash/alert) メッセージの到着。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_SMS\_の受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)構造を使用します。

<a name="remarks"></a>注釈
-------

RequestId は、新しいクラス-0 (flash/alert) メッセージの到着を示すために、ミニポートドライバーによって "0" に設定されます。 新しいクラス-0 (flash/alert) メッセージの到着は、現在のネットワーク登録状態に依存します。

読み取り要求によって、ミニポートドライバーの事前に割り当てられたバッファーで受け入れられない多数の SMS レコードが取得される場合、SMS レコードを複数の表示で MB サービスに送信できます。 この場合の uStatus は、\_SMS\_、中間トランザクションのデータをより多く\_データに\_設定する必要があります。また、最後のトランザクションは、WWAN\_STATUS\_SUCCESS で終了する必要があります。

次の図は、多数の SMS レコードを取得するための複数の表示方法を示しています。

![多数の sms レコードを取得するための複数の表示方法の使用方法を示す図](images/wwansmsrecordretrieval.png)

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


[OID\_WWAN\_SMS\_読み取り](oid-wwan-sms-read.md)

[**NDIS\_WWAN\_SMS\_受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)

 

 




