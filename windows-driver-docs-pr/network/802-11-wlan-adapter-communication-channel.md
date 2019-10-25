---
title: 802.11 WLAN アダプターの通信チャネル
description: 802.11 WLAN アダプターの通信チャネル
ms.assetid: 6a4b07a5-3a0a-41cb-a5cf-74d44fb38192
keywords:
- アダプター WDK 802.11 WLAN、通信チャネル
- WLAN アダプター WDK、通信チャネル
- 通信チャネルの WDK ネットワーク
- パススルー通信チャネル WDK ネットワーク
- パケット WDK ネットワーク、ネイティブ 802.11 IHV 拡張 DLL
- WDK ネイティブ 802.11 IHV 拡張 DLL を示す
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0237a172983b93d95389d8fb36df500ce97a9427
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838261"
---
# <a name="80211-wlan-adapter-communication-channel"></a>802.11 WLAN アダプターの通信チャネル




 

オペレーティングシステムは、IHV 拡張 DLL とネイティブ802.11 ミニポートドライバーの間にパススルー通信チャネルを提供します。 IHV 拡張 DLL は、次の操作のために通信チャネルにアクセスします。

<a href="" id="--------sending-receiving-proprietary-configuration-data"></a>**独自の構成データを送受信**する  
IHV 拡張 DLL は、 [**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数の呼び出しによって、NDIS 6.0 以降のオブジェクト識別子 (OID) メソッド要求をネイティブ802.11 ミニポートドライバーに送信します。 内部的には、この関数は、 [\_NIC\_特定の\_拡張機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-nic-specific-extension)をミニポートドライバーに\_、OID のメソッド要求を発行します。 NDIS OID メソッド要求の詳細については、「 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)」を参照してください。

通常、IHV Extensions DLL は**Dot11ExtNicSpecificExtension**を呼び出して、次の操作を実行します。

-   ミニポートドライバーまたは WLAN アダプターの固有の構成パラメーターを設定します。

-   専用の構成パラメーターまたはステータスデータをミニポートドライバーまたは WLAN アダプターから照会します。

<a href="" id="receiving-notifications-indications"></a>**通知/指示の受信**  
IHV 拡張 DLL は、 [*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) IHV ハンドラー関数の呼び出しによって、ネイティブ802.11 ミニポートドライバーから非同期的に通知を受信します。 オペレーティングシステムは、ミニポートドライバーが[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)の呼び出しによってメディア固有の指示を行うたびに、この関数を呼び出します。 この種類の表示の詳細については、「 [**NDIS\_STATUS\_MEDIA\_特定の\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-media-specific-indication)について」を参照してください。

<a href="" id="sending-802-11-packets"></a>**802.11 パケットの送信**  
IHV 拡張 DLL は、 [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)関数の呼び出しによって、802.11 パケットをネイティブ802.11 ミニポートドライバーに送信します。 ミニポートドライバーは、送信用の WLAN アダプターのパケットをキューに入れます。 パケットが送信されると、オペレーティングシステムは[*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) IHV ハンドラー関数を呼び出します。 IHV 拡張 DLL によるパケットの送信の詳細については、「[送信操作](send-operations.md)」を参照してください。

通常、IHV Extensions DLL は[**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)を呼び出して、関連付け後の操作中にセキュリティパケットを送信します。 セキュリティパケットは、DLL によってサポートされ、WLAN アダプターで有効になっている認証アルゴリズムに基づいています。

<a href="" id="receiving-802-11-packets"></a>**802.11 パケットの受信**  
IHV 拡張 DLL は、 [*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数の呼び出しによって、ネイティブ802.11 ミニポートドライバーから802.11 パケットを受信します。 オペレーティングシステムは、 [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出すことによって、DLL によって登録された EtherTypes の一覧のエントリと一致する IEEE EtherType を持つすべての受信パケットに対して、この関数を呼び出します。 IHV 拡張 DLL によるパケットの受信の詳細については、「[受信操作](receive-operations.md)」を参照してください。

次の点は、IHV 拡張 DLL とネイティブ802.11 ミニポートドライバーの間の通信チャネルに適用されます。

-   このチャネル経由で転送される構成、通知、または表示データには、独立系ハードウェアベンダー (IHV) によって定義された形式があります。これは、オペレーティングシステムに対して非透過的です。

-   このチャネルを介して受信されたすべてのデータは、IHV 拡張 DLL またはネイティブ802.11 ミニポートドライバーによって送信されたデータの順序でシリアル化および配信されます。

 

 





