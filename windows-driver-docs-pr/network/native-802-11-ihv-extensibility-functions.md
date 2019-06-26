---
title: ネイティブの 802.11 IHV 拡張関数
description: このセクションでは、ネイティブの 802.11 IHV 拡張 DLL の 802.11 IHV のネイティブ機能拡張機能がについて説明します
keywords:
- ネイティブの 802.11 IVH 拡張関数
- ネイティブ 802.11 IHV 拡張 DLL の機能拡張関数
- WDK ネイティブ 802.11 IVH 拡張関数
ms.assetid: 0E7CC153-5434-459D-9773-8CCAFBACD016
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ae755feda5de44a86eeb1129bbbb3d77ea7d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379406"
---
# <a name="native-80211-ihv-extensibility-functions"></a>ネイティブの 802.11 IHV 拡張関数

> [!IMPORTANT]
> [ネイティブ 802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスが Windows 10 以降非推奨とされます。 代わりに、WLAN デバイス ドライバー インターフェイス (WDI) を使用してください。 WDI の詳細については、次を参照してください。 [WLAN のユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)します。

802.11 IHV のネイティブ機能拡張関数では、オペレーティング システムによって提供されは、次の操作を IHV 拡張機能の DLL によって呼び出されます。

- 割り当てし、ネイティブの 802.11 フレームワーク内で使用されるバッファーを解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを経由の認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- 任意の認証および IHV の拡張機能の DLL によってサポートされている暗号アルゴリズムのさまざまなセキュリティ設定、IHV の WLAN のアダプターを構成します。
- IHV UI 拡張 dll (インストールされている) 場合イベント通知を処理するインターフェイスします。 たとえば、IHV 拡張機能の DLL は、基本的なサービスのセット (BSS) ネットワーク接続に関連するさまざまな段階について IHV UI 拡張機能の DLL を通知できます。 

IHV UI 拡張機能の DLL の詳細については、次を参照してください。[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)します。

> [!NOTE]
> IHV 拡張機能の DLL のメンバーに関連付けられている関数ポインターを通じて各ネイティブ 802.11 IHV 拡張関数を呼び出し、 [DOT11EXT_APIS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_apis)構造体。 オペレーティング システムを呼び出すと、 [Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV ハンドラー関数を使用して、IHV 拡張関数をポインターのリストを渡しますが、 *pDot11ExtAPI*パラメーター。
 
IHV 拡張機能の DLL によって呼び出すことができるネイティブ 802.11 IHV 拡張関数を次の表に示します。 IHV 機能拡張の各関数は、これらの条件下でのみ呼び出すことができます。


- **サービスの初期化後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 拡張機能の DLL を初期化するために、IHV ハンドラー関数が呼び出されました。 また、拡張 DLL が後 IHV 拡張関数を呼び出すことはできません、 [Dot11ExtIhvDeinitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV ハンドラー関数が呼び出されました。
- **アダプターの初期化後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvInitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV ハンドラー関数が呼び出されて、IHV の WLAN のアダプター インターフェイスを初期化します。  
IHV 拡張関数では、WLAN アダプターを識別するハンドルが必要です。 ときに*Dot11ExtIhvInitAdapter*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hDot11SvcHandle*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV ハンドラー関数が呼び出されました。
- **関連付け前後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvPerformPreAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV ハンドラー関数が呼び出されて基本サービスのセット (BSS) ネットワークとの関連付け前操作を開始します。  
IHV 拡張関数では、BSS ネットワーク接続を識別するハンドルが必要です。 ときに*Dot11ExtIhvPerformPreAssociate*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hConnection*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)または[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV ハンドラー関数が呼び出されています。
- **後のアソシエーションの後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvPerformPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV ハンドラー関数が呼び出されて基本サービスのセット (BSS) ネットワークと後の関連付け操作を開始します。  
IHV 拡張関数では、BSS のネットワーク接続でセキュリティ セッションを識別するハンドルが必要です。 ときに*Dot11ExtIhvPerformPostAssociate*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hSecuritySessionID*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)または[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV ハンドラー関数が呼び出されています。

| 関数 | サービスの初期化後に呼び出されます | アダプターの初期化後に呼び出されます | 関連付け前後に呼び出されます | 後のアソシエーションの後に呼び出されます |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_allocate_buffer) | x |   |   |   |
| [Dot11ExtFreeBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_free_buffer) | x |   |   |   |
| [Dot11ExtGetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data) |   |   | x |   | 
| [Dot11ExtNicSpecificExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) |   | x |   |   |
| [Dot11ExtStartOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_start) |   |   |   | x |
| [Dot11ExtStopOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_stop) |   |   |   | x |
| [Dot11ExtPostAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) |   |   |   | x |
| [Dot11ExtPreAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) |   |   | x |   |
| [Dot11ExtProcessOneXPacket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_process_onex_packet) |   |   |   | x |
| [Dot11ExtQueryVirtualStationProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties) |   | x |   |   |
| [Dot11ExtReleaseVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_release_virtual_station) |   | x |   |   |
| [Dot11ExtRequestVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_request_virtual_station) |   | x |   |   |
| [Dot11ExtSendNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification) |   | x |   |   |
| [Dot11ExtSendUIRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) |   | x |   |   |
| [Dot11ExtSetAuthAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm) |   | x |   |   |
| [Dot11ExtSetCurrentProfile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_current_profile) |   |   | x |   |
| [Dot11ExtSetDefaultKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key) |   | x |   |   |
| [Dot11ExtSetDefaultKeyId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)|   | x |   |   |
| [Dot11ExtSetEtherTypeHandling](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) |   | x |   |   |
| [Dot11ExtSetExcludeUnencrypted](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) |   | x |   |   |
| [Dot11ExtSetKeyMappingKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key) |   | x |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm) |   | x |   |   |
| [Dot11ExtSetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data) |   | x |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm) |   | x |   |   |
| [Dot11ExtSetVirtualStationAPProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties) |   |   | x |   | 

IHV ハンドラー関数の詳細については、次を参照してください。 [802.11 IHV ハンドラー関数をネイティブ](native-802-11-ihv-handler-functions.md)します。


