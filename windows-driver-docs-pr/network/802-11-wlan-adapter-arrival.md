---
title: 802.11 WLAN アダプターの接続
description: 802.11 WLAN アダプターの接続
ms.assetid: 4d533f32-0f98-4a65-ac1b-7a470e54ad29
keywords:
- アダプター WDK 802.11 WLAN、到着
- WLAN アダプター WDK、到着
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8afa6fa1aed3e0e56b53aa6962ee516bb1a171e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838264"
---
# <a name="80211-wlan-adapter-arrival"></a>802.11 WLAN アダプターの接続




 

IHV 拡張 DLL がインストールされているワイヤレス LAN (WLAN) アダプターがオペレーティングシステムによって検出されると、オペレーティングシステムは[*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV ハンドラー関数を呼び出します。 オペレーティングシステムは、ワイヤレスアダプターが挿入されたときなど、WLAN アダプターが使用可能になり、使用できるようになるたびに、この機能を呼び出します。

[*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)関数が呼び出されると、IHV 拡張 DLL は次のことを実行します。

-   WLAN アダプターのコンテキストデータの配列、およびその DLL が WLAN アダプターに必要とするすべてのリソースを割り当てます。

-   IHV 拡張 DLL によって受信および使用されるセキュリティパケットの IEEE EtherTypes の一覧を登録します。

-   IHV によって定義された独自の設定を使用してアダプタを構成します。

[*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)が呼び出された場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   *HDot11SvcHandle*パラメーターには、WLAN アダプターのオペレーティングシステムによって割り当てられた一意のハンドル値が含まれています。 IHV 拡張 DLL は、このハンドル値を保存し、 [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)などのアダプター固有の処理に関連する IHV 拡張関数の*hDot11SvcHandle*パラメーターに渡す必要があります。

    通常、DLL は、このハンドル値を WLAN アダプターコンテキスト配列のメンバー内に保存します。

-   IHV 拡張 DLL は、 *phIhvExtAdapter*パラメーターを使用して、WLAN アダプターの一意のハンドル値を返す必要があります。 オペレーティングシステムは、 [*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)などのアダプター固有の処理に関連する IHV ハンドラー関数の*Hihvextadapter*パラメーターにハンドル値を渡します。

    通常、DLL は、WLAN アダプターのコンテキスト配列のアドレスをハンドル値として返します。

-   IHV Extensions DLL は、 [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出して、DLL が受信するセキュリティパケットの IEEE EtherTypes の一覧を登録します。 また、IHV Extensions DLL は、ペイロードの暗号化解除から除外される EtherTypes の一覧を指定することもできます。 EtherTypes の登録の詳細については、「 [IEEE EtherType の処理](ieee-ethertype-handling.md)」を参照してください。

    EtherTypes が登録されると、オペレーティングシステムは、EtherType がリスト内のエントリと一致するすべてのパケットに対して[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV ハンドラー関数を呼び出します。

-   オペレーティングシステムは、ネイティブ802.11 オブジェクト識別子 (Oid) の set 要求を通じて、標準の802.11 パラメーターを使用してアダプターを構成します。 これらの Oid の詳細については、「[ネイティブ802.11 ワイヤレス LAN oid](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-oids)」を参照してください。

    ただし、DLL では、 [**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数を呼び出すことによって、独自のパラメーターを使用してアダプターを構成できます。 この関数呼び出しを使用すると、DLL は、WLAN アダプターを管理してクエリを発行したり、IHV によって定義された専用形式に基づいてドライバーに要求を設定したりするネイティブ802.11 ミニポートドライバーと直接通信できます。

    DLL および WLAN アダプターが通信するインターフェイスの詳細については、「 [802.11 WLAN アダプター通信チャネル](802-11-wlan-adapter-communication-channel.md)」を参照してください。

 

 





