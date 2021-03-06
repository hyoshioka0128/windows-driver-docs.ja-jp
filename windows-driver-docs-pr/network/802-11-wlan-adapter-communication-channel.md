---
title: 802.11 WLAN アダプターの通信チャネル
description: 802.11 WLAN アダプターの通信チャネル
ms.assetid: 6a4b07a5-3a0a-41cb-a5cf-74d44fb38192
keywords:
- アダプター WDK 802.11 WLAN、通信チャネル
- WLAN アダプター WDK、通信チャネル
- 通信チャネルの WDK ネットワーク
- パススルー通信チャネルの WDK ネットワーク
- パケット WDK ネットワー キング、ネイティブの 802.11 IHV 拡張 DLL
- WDK の 802.11 IHV ・拡張機能のネイティブ DLL がないです。
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f09c799b57bb809c47fa2b82b147a485ea28b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379316"
---
# <a name="80211-wlan-adapter-communication-channel"></a>802.11 WLAN アダプターの通信チャネル




 

オペレーティング システムでは、IHV 拡張機能の DLL とネイティブの 802.11 ミニポート ドライバーの間の通信のパススルー チャネルを提供します。 IHV 拡張機能の DLL では、次の操作用の通信チャネルにアクセスします。

<a href="" id="--------sending-receiving-proprietary-configuration-data"></a> **データの送信/受信専用の構成**  
IHV 拡張機能の DLL NDIS 6.0 またはそれ以降のオブジェクト識別子 (OID) メソッドは要求を送信呼び出しを通じてネイティブ 802.11 ミニポート ドライバー、 [ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数。 この関数が内部的には、メソッドの要求を発行[OID\_DOT11\_NIC\_特定\_拡張子](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-nic-specific-extension)ミニポート ドライバーにします。 NDIS OID メソッド要求の詳細については、次を参照してください。 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)します。

IHV 拡張機能の DLL の呼び出しでは通常、 **Dot11ExtNicSpecificExtension**以下を実行します。

-   ミニポート ドライバーまたは WLAN アダプターに専用の構成パラメーターを設定します。

-   専用の構成パラメーターまたはミニポート ドライバーまたは WLAN アダプターからの状態データをクエリします。

<a href="" id="receiving-notifications-indications"></a>**受信通知/問題**  
IHV 拡張機能の DLL は非同期的に呼び出しを通じてネイティブ 802.11 ミニポート ドライバーから通知を受け取る、 [ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication) IHV ハンドラー関数。 ミニポート ドライバーを呼び出すことによって、特定のメディアを示す値を使用するたびに、オペレーティング システムがこの関数を呼び出す[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 この種類の表示の詳細については、次を参照してください。 [ **NDIS\_状態\_メディア\_特定\_INDICATION**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-media-specific-indication)。

<a href="" id="sending-802-11-packets"></a>**802.11 パケットを送信します。**  
IHV 拡張 DLL の呼び出しを通じてネイティブ 802.11 ミニポート ドライバーに 802.11 のパケットを送信します、 [ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)関数。 ミニポート ドライバーでは、WLAN アダプターの送信パケットをキューします。 パケットが送信されたときに、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvSendPacketCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) IHV ハンドラー関数。 IHV 拡張 DLL でパケットを送信する詳細については、次を参照してください。[送信操作](send-operations.md)します。

IHV 拡張機能の DLL の呼び出しでは通常、 [ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)後関連付け操作中にセキュリティのパケットを送信します。 セキュリティのパケットは、DLL でサポートされているし、WLAN アダプターで有効になっている認証アルゴリズムに基づいています。

<a href="" id="receiving-802-11-packets"></a>**802.11 パケットの受信**  
IHV 拡張機能の DLL は、呼び出しを通じてネイティブ 802.11 ミニポート ドライバーから 802.11 パケットを受信、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数。 オペレーティング システムでは、この関数を呼び出すを呼び出すことによって、DLL によって登録された EtherTypes のリスト内のエントリに一致する IEEE EtherType のあるすべての受信パケットの[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling). IHV 拡張機能の DLL によってパケットの受信の詳細については、次を参照してください。[受信操作](receive-operations.md)します。

次の点は、IHV 拡張機能の DLL とネイティブの 802.11 ミニポート ドライバー間の通信チャネルに適用されます。

-   構成、通知、またはこのチャネル経由で転送されたデータを示す値がオペレーティング システムに不透明である独立系ハードウェア ベンダー (IHV) によって定義された形式があります。

-   このチャネル経由で受信したすべてのデータがシリアル化され、IHV 拡張機能の DLL またはネイティブの 802.11 ミニポート ドライバーによってデータが送信された順序どおりに配信します。

 

 





