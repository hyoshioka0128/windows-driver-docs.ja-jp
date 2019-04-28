---
title: NDIS_STATUS_WWAN_PACKET_SERVICE
description: ミニポート ドライバーでは、パケットは、現在使用されているパケット データ サービスの種類の変更を通知するのになど、可用性の変更をサービスするときに、MB サービスに通知するのに NDIS_STATUS_WWAN_PACKET_SERVICE 通知を使用します。
ms.assetid: 7a04b54e-e07b-43dc-ba76-086d7521ff60
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PACKET_SERVICE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1cbbe32663674087b7e50ff607c01860efc55ab4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369876"
---
# <a name="ndisstatuswwanpacketservice"></a>NDIS\_状態\_WWAN\_パケット\_サービス


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_パケット\_パケットのパケット データの種類の変更を通知するなど、可用性の変更をサービスするときに、サービスに MB を通知サービスの通知現在使用されているサービスです。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_パケット\_サービス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567910)構造体。

<a name="remarks"></a>注釈
-------

CDMA ベースのミニポート ドライバーを自動的に開始できるパケットの場合に接続サービスがリソース割り当て/解放しない可能性があり、MB サービスにイベント通知を送信することができます。

ミニポート ドライバーは、イベント通知に関する次のガイドラインに従う必要があります。

-   ミニポート ドライバーを設定する必要があります**AvailableDataClasses** WWAN に設定されている\_データ\_クラス\_ミニポート ドライバーの初期化時に NONE。 その後、ミニポート ドライバーする必要がありますサービスに通知 MB に変更があるたびに**AvailableDataClasses**します。

-   ミニポート ドライバーを設定する必要があります**CurrentDataClass** WWAN に\_データ\_クラス\_ミニポート ドライバーの初期化時に NONE。 その後、ミニポート ドライバーする必要がありますサービスに通知 MB に変更があるたびに**CurrentDataClass**します。 ミニポート ドライバーは、NDIS を送信する必要があります\_状態\_リンク\_状態通知の場合に変更**CurrentDataClass**送信変更されます。 または、リンク速度を受信します。

-   パケットのサービスでの変更状態の接続がある場合に、ミニポート ドライバーは MB サービスに通知する必要があります。

ミニポート ドライバーに返す必要があります*クエリ*次の規則に従って結果。

-   ミニポート ドライバーが WWAN を返す必要があります\_状態\_成功**WwanPacketServiceStateAttaching**デバイスがパケットをアタッチしようとしたときにします。

-   ミニポート ドライバーが WWAN を返す必要があります\_状態\_成功**WwanPacketServiceStateDetaching**デバイスがパケット デタッチしようとしたときにします。

-   デバイスは、最終的な状態では、ミニポート ドライバーは WWAN を返す必要があります\_状態\_適切な現在の状態と共に成功 ( **WwanPacketServiceStateAttached**または**WwanPacketServiceStateDetached**)

-   ミニポート ドライバーする必要がありますクラスの一覧をすべて使用可能なデータのです。だけでなく、最高データ クラス使用できます。 両方に適用*クエリ*イベント通知と同様に操作します。

ミニポート ドライバーに返す必要があります*設定*次の規則に従って結果。

-   WWAN を返す\_状態\_成功すると場合、*設定*で要求**WwanPacketServiceActionAttach**、サービスによって発行されると、デバイスがパケットに接続された状態で既に。

-   WWAN を返す\_状態\_成功すると場合、*設定*の要求**WwanPacketServiceActionDetach**、サービスによって発行されると、デバイスがパケットからデタッチされた状態で既に。

-   一時的な状態を返すことはありません、*設定*要求。 最終状態のみ**WwanPacketServiceStateAttached**または**WwanPacketServiceStateDetached** WWANでパケットのサービス操作を正常に完了した後に返す必要がある\_状態\_成功

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


[**NDIS\_WWAN\_パケット\_サービス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567910)

[OID\_WWAN\_パケット\_サービス](oid-wwan-packet-service.md)

 

 




