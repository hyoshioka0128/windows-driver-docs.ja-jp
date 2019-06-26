---
title: ネイティブの 802.11 IHV ハンドラー関数
description: このセクションでは、ネイティブの 802.11 IHV 拡張 DLL のネイティブの 802.11 IHV ハンドラー関数がについて説明します
keywords:
- ネイティブの 802.11 IVH ハンドラー関数
- ネイティブ 802.11 IHV 拡張 DLL ハンドラー関数
- WDK ネイティブ 802.11 IVH ハンドラー関数
ms.assetid: BF0DC1C7-48E1-487E-8F64-146BBA322F40
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bafaec6d047925a94e9072ed5e84660ef29b1d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387285"
---
# <a name="native-80211-ihv-handler-functions"></a>ネイティブの 802.11 IHV ハンドラー関数

>[!IMPORTANT]
> [ネイティブ 802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスが Windows 10 以降非推奨とされます。 代わりに、WLAN デバイス ドライバー インターフェイス (WDI) を使用してください。 WDI の詳細については、次を参照してください。 [WLAN のユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)します。

ネイティブの 802.11 IHV ハンドラー関数は、IHV 拡張機能の DLL によって提供されには、次のオペレーティング システムによって呼び出されます。

- 割り当てし、ネイティブの 802.11 フレームワーク内で使用されるバッファーを解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを経由の認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- 指定された一連の IEEE EtherType 値とプライバシーの除外規則に基づいてパケットが表示されます。
- IHV の WLAN のアダプターを構成するには、独自の認証と暗号アルゴリズムのさまざまなセキュリティ設定。
- IHV UI 拡張 dll (インストールされている) 場合イベント通知を処理するインターフェイスします。 たとえば、IHV 拡張機能の DLL は、基本的なサービスのセット (BSS) ネットワーク接続に関連するさまざまな段階について UI 拡張機能の DLL を通知できます。 

IHV UI 拡張機能の DLL の詳細については、次を参照してください。[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)します。

> [!NOTE]
> 例外として[Dot11ExtIhvGetVersionInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)と[Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)、オペレーティング システムは、のメンバーに関連付けられている、関数ポインターを通じてIHVハンドラー関数を呼び出します。[DOT11EXT_IHV_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)構造体。 オペレーティング システムを呼び出すと、 *Dot11ExtIhvInitService* IHV ハンドラー関数で IHV 拡張機能の DLL を使用して、IHV ハンドラー関数をポインターのリストが返されます、 *pDot11IHVHandlers*パラメーター。

このセクションでは、次のネイティブの 802.11 IHV ハンドラー関数について説明します。

- [Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)
- [Dot11ExtIhvControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_control)
- [Dot11ExtIhvCreateDiscoveryProfiles](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles)
- [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)
- [Dot11ExtIhvDeinitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_service)
- [Dot11ExtIhvGetVersionInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info)
- [Dot11ExtIhvInitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)
- [Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)
- [Dot11ExtIhvInitVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station)
- [Dot11ExtIhvIsUIRequestPending](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)
- [Dot11ExtIhvOneXIndicateResult](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)
- [Dot11ExtIhvPerformCapabilityMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)
- [Dot11ExtIhvPerformPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)
- [Dot11ExtIhvPerformPreAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)
- [Dot11ExtIhvProcessSessionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_session_change)
- [Dot11ExtIhvProcessUIResponse](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)
- [Dot11ExtIhvQueryUIRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)
- [Dot11ExtIhvReceiveIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication)
- [Dot11ExtIhvReceivePacket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)
- [Dot11ExtIhvSendPacketCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)
- [Dot11ExtIhvStopPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)
- [Dot11ExtIhvValidateProfile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_validate_profile)

