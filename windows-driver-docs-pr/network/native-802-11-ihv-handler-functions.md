---
title: ネイティブ 802.11 IHV ハンドラー関数
description: このセクションでは、ネイティブ 802.11 IHV 拡張 DLL 用のネイティブ 802.11 IHV ハンドラー関数について説明します。
keywords:
- ネイティブ 802.11 IVH Handler 関数
- ネイティブ 802.11 IHV 拡張 DLL ハンドラー関数
- WDK ネイティブ 802.11 IVH Handler 関数
ms.assetid: BF0DC1C7-48E1-487E-8F64-146BBA322F40
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 462c921233b0d6a15c391cc27db225897b55c0ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839639"
---
# <a name="native-80211-ihv-handler-functions"></a>ネイティブ 802.11 IHV ハンドラー関数

>[!IMPORTANT]
> [ネイティブ802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスは、Windows 10 以降では非推奨とされます。 代わりに、WLAN デバイスドライバーインターフェイス (WDI) を使用してください。 WDI の詳細については、「 [WLAN ユニバーサル Windows ドライバーモデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)」を参照してください。

ネイティブ 802.11 IHV ハンドラー関数は、IHV 拡張 DLL によって提供され、オペレーティングシステムによって次の処理を実行するために呼び出されます。

- ネイティブ802.11 フレームワーク内で使用されるバッファーを割り当て、解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを介して、認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- 指定された IEEE EtherType 値とプライバシー除外規則の一覧に基づいてパケットを受信します。
- 独自の認証および暗号アルゴリズムに対してさまざまなセキュリティ設定を使用して、IHV の WLAN アダプターを構成します。
- イベント通知を処理するために、IHV UI Extensions DLL (インストールされている場合) を使用したインターフェイス。 たとえば、IHV 拡張 DLL は、基本サービスセット (BSS) のネットワーク接続に関連するさまざまな段階について、UI 拡張 DLL に通知することができます。 

IHV UI 拡張 DLL の詳細については、「[ネイティブ 802.11 IHV Ui EXTENSIONS dll](native-802-11-ihv-ui-extensions-dll2.md)」を参照してください。

> [!NOTE]
> [Dot11ExtIhvGetVersionInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)と[Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)を除き、オペレーティングシステムは、 [DOT11EXT_IHV_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)構造体のメンバーに関連付けられている関数ポインターを介して IHV ハンドラー関数を呼び出します。 オペレーティングシステムが*Dot11ExtIhvInitService* IHV ハンドラー関数を呼び出すと、IHV 拡張 DLL は、 *pDot11IHVHandlers*パラメーターを使用して、ihv ハンドラー関数へのポインターの一覧を返します。

このセクションでは、次のネイティブ 802.11 IHV ハンドラー関数について説明します。

- [Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)
- [Dot11ExtIhvControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_control)
- [Dot11ExtIhvCreateDiscoveryProfiles](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles)
- [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)
- [Dot11ExtIhvDeinitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service)
- [Dot11ExtIhvGetVersionInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)
- [Dot11ExtIhvInitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)
- [Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)
- [Dot11ExtIhvInitVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station)
- [Dot11ExtIhvIsUIRequestPending](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)
- [Dot11ExtIhvOneXIndicateResult](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)
- [Dot11ExtIhvPerformCapabilityMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)
- [Dot11ExtIhvPerformPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)
- [Dot11ExtIhvPerformPreAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)
- [Dot11ExtIhvProcessSessionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change)
- [Dot11ExtIhvProcessUIResponse](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)
- [Dot11ExtIhvQueryUIRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)
- [Dot11ExtIhvReceiveIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)
- [Dot11ExtIhvReceivePacket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)
- [Dot11ExtIhvSendPacketCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)
- [Dot11ExtIhvStopPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)
- [Dot11ExtIhvValidateProfile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_validate_profile)

