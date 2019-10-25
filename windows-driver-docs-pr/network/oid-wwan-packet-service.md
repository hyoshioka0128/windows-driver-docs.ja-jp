---
title: OID_WWAN_PACKET_SERVICE
description: OID_WWAN_PACKET_SERVICE は、GSM ベースのデバイスと CDMA ベースの MB デバイスの両方について、現在登録されているプロバイダーのネットワークに対して、パケットサービスのアタッチ/デタッチ操作を実行するようにミニポートドライバーに指示するために使用されます。
ms.assetid: 97bb9324-8052-437c-baa5-fb9a8176c779
ms.date: 04/04/2019
keywords: -Windows Vista 以降の OID_WWAN_PACKET_SERVICE ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ee44aacaab4fdae455f57036c0171e975ff1fa31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843823"
---
# <a name="oid_wwan_packet_service"></a>OID\_WWAN\_パケット\_サービス


OID\_WWAN\_パケット\_サービスを使用して、GSM ベースのデバイスと CDMA ベースの MB デバイスの両方について、現在登録されているプロバイダーのネットワークでパケットサービスのアタッチ/デタッチアクションを実行するようにミニポートドライバーに指示します。 この OID は、パケットサービスのアタッチ/デタッチの状態に加えて、データクラスの可用性と現在使用されているデータクラスの情報を決定するために使用されます。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_パケットに送信する必要があり @no**](ndis-status-wwan-packet-service.md)set 要求またはクエリ要求の完了に関係なく現在のパケットサービスの状態に関する情報を提供する[**NDIS\_WWAN\_パケット\_サービス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)構造を含む、サービス状態通知.

現在のパケットサービスの状態を設定するように要求している呼び出し元は、 [**NDIS\_WWAN\_\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)構造をミニポートドライバーに設定し、適切な情報を提供します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN パケットサービスのアタッチ操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)」を参照してください。

ミニポートドライバーは、クエリまたはセット操作を処理するときにプロバイダーネットワークにアクセスできますが、サブスクライバー Id モジュール (SIM カード) にはアクセスできません。

CDMA ベースのデバイスは、可能であれば、これをネットワークリソースの割り当てを解放する機会として使用する必要があります。

一部の SIM カードを使用すると、MB デバイスは、サーキットスイッチドメインではなく、パケットドメインにのみ登録できます。 データ呼び出しが終了すると、VAN UI は OID\_WWAN\_パケット\_サービスセット要求を送信してパケットサービスをデタッチします。 これにより、MB デバイスがパケットドメインから切断されます。 MB デバイスはネットワークから登録解除され、省電力モードになります。 その結果、デバイスは、登録が解除された結果として VAN UI から消え、再起動することによってのみ回復できます。 このシナリオでは、ミニポートドライバーは、MB デバイスをこのようなモードに設定せずに正のデータを返すことにより、パケットのアタッチ/デタッチ操作をスプーフィングする必要があります。

パケット接続をサポートしていないテクノロジの場合、ミニポートドライバーは、コンテキストのアクティブ化を続行できることを MB サービスに通知するために、接続状態を偽装する必要があります。 また、ミニポートドライバーは、ミニポートドライバーで\_パケット\_サービス要求の OID\_設定します。 ミニポートドライバーは、クエリ操作および要請されていないイベントに対して、 [ **\_パケット\_サービスの通知\_NDIS\_ステータス**](ndis-status-wwan-packet-service.md)を送信する必要があります。 デバイスパケットサービスの状態が*Wwanpacketservicestateattached*設定されていない場合、ミニポートドライバーは PDP のアクティブ化を失敗させる必要があります。

この MB サービスは、パケットサービスの状態が*Wwanpacketservicestateattached*達しない限り、コンテキストのアクティブ化を続行できません。

### <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

この OID の新しいリビジョン2は、Windows 10 バージョン1903以降でサポートされています。 この拡張機能により、ホストは、5G で現在動作している周波数範囲に対してクエリを実行できるようになります。

ホストは、拡張パケットサービスの状態情報をいつでも照会できます。 この応答はリビジョン1と同じですが、リビジョン2には2つの新しいフィールドがあります。

モデムが5G ドメインに登録されている場合は、通信事業者の 5G frequency 範囲が返されます。 複数の 5G carrier が存在する場合は、すべての有効な範囲が返されます。

5G data クラスのサポートの詳細については、「 [MB 5G データクラスのサポート](mb-5g-data-class-support.md)」を参照してください。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_\_パケット\_サービスの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)

[**NDIS\_ステータス\_WWAN\_パケット\_サービス**](ndis-status-wwan-packet-service.md)

[WWAN パケットサービスのアタッチ操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)

 

 




