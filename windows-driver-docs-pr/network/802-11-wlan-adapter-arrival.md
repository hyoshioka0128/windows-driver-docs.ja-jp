---
title: 802.11 WLAN アダプターの接続
description: 802.11 WLAN アダプターの接続
ms.assetid: 4d533f32-0f98-4a65-ac1b-7a470e54ad29
keywords:
- WDK 802.11 WLAN、到着のアダプター
- WLAN アダプター WDK、到着
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7bb676d2760550647c7d3e966cc851ba0c00ef8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379313"
---
# <a name="80211-wlan-adapter-arrival"></a>802.11 WLAN アダプターの接続




 

オペレーティング システムでは、IHV の拡張 DLL がインストールされているワイヤレス LAN (WLAN) アダプターを検出すると、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV ハンドラー関数。 オペレーティング システム関数を呼び出しますこの WLAN アダプターになるたびに有効になっていますなど PCMCIA アダプターが挿入されると、使用するためです。

ときに、 [ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)関数が呼び出されると、IHV 拡張機能の DLL は、次を実行します。

-   WLAN アダプターの DLL が必要なすべてのリソースと同様に、WLAN アダプター コンテキスト データの配列を割り当てます。

-   受信され、IHV 拡張機能の DLL によって使用されるセキュリティ パケットに IEEE EtherTypes の一覧を登録します。

-   独自の設定を IHV で定義されているとアダプターを構成します。

IHV 拡張機能の DLL が次のガイドラインに従う必要がありますと[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)が呼び出されます。

-   *HDot11SvcHandle*パラメーターには、WLAN アダプター用のオペレーティング システムによって割り当てられる一意のハンドル値が含まれています。 IHV 拡張機能の DLL は、このハンドルの値を保存する必要がありますに渡すと、 *hDot11SvcHandle* IHV 拡張関数のパラメーターなどのアダプター固有の処理に関連[ **Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)します。

    通常、DLL は、その WLAN アダプター コンテキスト配列のメンバー内には、このハンドル値を保存します。

-   IHV 拡張機能の DLL を使って WLAN アダプターに固有のハンドル値を返す必要があります、 *phIhvExtAdapter*パラメーター。 オペレーティング システムへのハンドル値を渡します、 *hIhvExtAdapter* IHV ハンドラー関数のパラメーターなどのアダプター固有の処理に関連[ *Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication).

    通常、DLL は、ハンドル値として WLAN アダプター コンテキストの配列のアドレスを返します。

-   拡張 DLL の IHV 呼び出し[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) DLL を受信するセキュリティ パケットに IEEE EtherTypes の一覧を登録します。 IHV 拡張機能の DLL には、一連のペイロードの暗号化解除を除外 EtherTypes も指定できます。 EtherTypes の登録の詳細については、次を参照してください。 [IEEE EtherType 処理](ieee-ethertype-handling.md)します。

    EtherTypes が登録されると、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)が EtherType には、リスト内のエントリが一致するすべてのパケットの IHV ハンドラー関数。

-   オペレーティング システムでは、ネイティブ 802.11 オブジェクト識別子 (Oid) のセット要求を通じた 802.11 標準のパラメーターに、アダプターを構成します。 これらの Oid の詳細については、次を参照してください。[ネイティブ 802.11 ワイヤレス LAN の Oid](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-oids)します。

    ただし、DLL は、呼び出しを通じて独自のパラメーターを持つのアダプターを構成できます、 [ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数。 この関数の呼び出しを通じて DLL は、WLAN アダプターとクエリの問題を管理するネイティブの 802.11 ミニポート ドライバーと直接通信または要求を IHV によって定義された独自の形式に基づくドライバーに設定します。

    DLL および WLAN のアダプターの通信インターフェイスの詳細については、次を参照してください。 [802.11 WLAN アダプターの通信チャネル](802-11-wlan-adapter-communication-channel.md)します。

 

 





