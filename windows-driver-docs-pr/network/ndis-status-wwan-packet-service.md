---
title: NDIS_STATUS_WWAN_PACKET_SERVICE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PACKET_SERVICE 通知を使用して、現在使用されているパケットデータサービスの種類への変更を通知するなど、パケットサービスの可用性が変化したときに MB サービスに通知します。
ms.assetid: 7a04b54e-e07b-43dc-ba76-086d7521ff60
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_PACKET_SERVICE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e12f5906cfad6030b88cd5615e289c6e19531597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844760"
---
# <a name="ndis_status_wwan_packet_service"></a>NDIS\_ステータス\_WWAN\_パケット\_サービス


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_パケット\_サービス通知を使用して、現在使用されているパケットデータサービスの種類への変更を通知するなど、パケットサービスの可用性が変化したときに MB サービスに通知します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_パケット\_サービス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)構造を使用します。

<a name="remarks"></a>注釈
-------

CDMA ベースのミニポートドライバーは、リソースの割り当て/解放が可能でない場合にパケットアタッチサービスを自動的に開始し、MB サービスにイベント通知を送信できます。

ミニポートドライバーは、イベント通知に関する次のガイドラインに従う必要があります。

-   ミニポートドライバーは、ミニポートドライバーの初期化中に、[指定されたデータ\_クラス\_しない] を [WWAN\_データ**に設定する**] を設定する必要があります。 その後、空きポートドライバーは、空き**Dataclを**変更するたびに、MB サービスに通知する必要があります。

-   ミニポートドライバーは、ミニポートドライバーの初期化中に、 **CurrentDataClass**を WWAN\_DATA\_クラス\_設定する必要があります。 その後、 **CurrentDataClass**に変更があった場合は常に、ミニポートドライバーが MB サービスに通知する必要があります。 **CurrentDataClass**への変更によって送信または受信リンク速度が変更された場合、ミニポートドライバーは NDIS\_状態\_リンク\_状態通知を送信する必要があります。

-   ミニポートドライバーは、パケットサービスのアタッチ状態が変更されるたびに、MB サービスに通知する必要があります。

ミニポートドライバーは、次の規則に従って*クエリ*の結果を返す必要があります。

-   ミニポートドライバーは、デバイスがパケット接続を試行するたびに、 **Wwanpacketservicestateattaching**で WWAN\_の状態\_SUCCESS を返す必要があります。

-   デバイスがパケットを切断しようとするたびに、ミニポートドライバーは、 **Wwanpacketservicestatedetaching**で WWAN\_の状態\_SUCCESS を返す必要があります。

-   デバイスが最終状態になると、ミニポートドライバーは、適切な現在の状態と共に、WWAN\_STATUS\_SUCCESS を返す必要があります ( **Wwanpacketservicestateattached**または**Wwanpacketservicestateattached はデタッチ**されています)。

-   ミニポートドライバーは、使用可能なすべてのデータクラスを一覧表示する必要があります。使用可能な最高のデータクラスだけではありません。 これは、*クエリ*操作とイベント通知の両方に適用されます。

ミニポートドライバーは、次の規則に従って*設定*された結果を返す必要があります。

-   **Wwanpacketserviceactionattach**で*Set* request がサービスによって発行され、デバイスが既にパケット接続されている状態になっている場合、WWAN\_STATUS\_SUCCESS を返します。

-   **Wwanpacketserviceactiondetach**による*Set*要求がサービスによって発行され、デバイスが既にパケットデタッチ状態になっている場合、WWAN\_STATUS\_SUCCESS が返されます。

-   *Set*要求の一時的な状態を返しません。 WWAN\_ステータス\_成功したパケットサービス操作が正常に完了した後に返される必要があるのは、最後の状態である**Wwanpacketservicestateattached**または**wwanpacketservicestateattached**場合のみです。

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


[**NDIS\_WWAN\_パケット\_サービス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)

[OID\_WWAN\_パケット\_サービス](oid-wwan-packet-service.md)

 

 




