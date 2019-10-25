---
title: ネイティブ 802.11 IHV 拡張関数
description: このセクションでは、ネイティブ 802.11 IHV 拡張 DLL 用のネイティブ 802.11 IHV 拡張機能について説明します。
keywords:
- ネイティブ 802.11 IVH 機能拡張関数
- ネイティブ 802.11 IHV 拡張 DLL の拡張関数
- WDK ネイティブ 802.11 IVH 機能拡張関数
ms.assetid: 0E7CC153-5434-459D-9773-8CCAFBACD016
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: abafb090217640560948cc7474d3aa5ad535605a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844207"
---
# <a name="native-80211-ihv-extensibility-functions"></a>ネイティブ 802.11 IHV 拡張関数

> [!IMPORTANT]
> [ネイティブ802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスは、Windows 10 以降では非推奨とされます。 代わりに、WLAN デバイスドライバーインターフェイス (WDI) を使用してください。 WDI の詳細については、「 [WLAN ユニバーサル Windows ドライバーモデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)」を参照してください。

ネイティブ 802.11 IHV 拡張関数はオペレーティングシステムによって提供され、次の操作を行うために IHV 拡張 DLL によって呼び出されます。

- ネイティブ802.11 フレームワーク内で使用されるバッファーを割り当て、解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを介して、認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- Ihv 拡張 DLL でサポートされている認証アルゴリズムと暗号アルゴリズムのさまざまなセキュリティ設定を使用して、IHV の WLAN アダプターを構成します。
- イベント通知を処理するために、IHV UI Extensions DLL (インストールされている場合) を使用したインターフェイス。 たとえば、IHV 拡張 DLL は、基本サービスセット (BSS) のネットワーク接続に関連するさまざまな段階について、IHV UI 拡張 DLL に通知できます。 

IHV UI 拡張 DLL の詳細については、「[ネイティブ 802.11 IHV Ui EXTENSIONS dll](native-802-11-ihv-ui-extensions-dll2.md)」を参照してください。

> [!NOTE]
> IHV Extensions DLL は、 [DOT11EXT_APIS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_apis)構造体のメンバーに関連付けられている関数ポインターを介して、各ネイティブ 802.11 IHV 拡張関数を呼び出します。 オペレーティングシステムは、 [Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) ihv ハンドラー関数を呼び出すと、 *pDot11ExtAPI*パラメーターを使用して、IHV 機能拡張関数へのポインターのリストを渡します。
 
次の表は、IHV 拡張 DLL によって呼び出すことができるネイティブ 802.11 IHV 拡張関数を示しています。 各 IHV 機能拡張関数は、これらの条件下でのみ呼び出すことができます。


- **サービスの初期化後に呼び出されます。**  
IHV 拡張関数を呼び出すことができるのは、IHV 拡張 DLL を初期化するために[Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV ハンドラー関数が呼び出された後のみです。 また、 [Dot11ExtIhvDeinitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) ihv ハンドラー関数が呼び出された後に、Extensions DLL が IHV 拡張関数を呼び出すことはできません。
- **アダプターの初期化後に呼び出されます。**  
IHV 機能拡張関数は、IHV の WLAN アダプターへのインターフェイスを初期化するために、 [Dot11ExtIhvInitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV ハンドラー関数が呼び出された後にのみ呼び出すことができます。  
IHV 機能拡張機能には、WLAN アダプターを識別するハンドルが必要です。 *Dot11ExtIhvInitAdapter*が呼び出されると、IHV 拡張 DLL は*hDot11SvcHandle*パラメーターを介してこのハンドルに渡されます。  
[Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) ihv ハンドラー関数が呼び出された後に、Extensions DLL が IHV 拡張関数を呼び出すことはできません。
- **事前関連付けの後に呼び出されます。**  
IHV 拡張関数は、基本サービスセット (BSS) ネットワークでの関連付け前の操作を開始するために[Dot11ExtIhvPerformPreAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV ハンドラー関数が呼び出された後にのみ呼び出すことができます。  
IHV 拡張関数には、BSS ネットワーク接続を識別するハンドルが必要です。 *Dot11ExtIhvPerformPreAssociate*が呼び出されると、IHV 拡張 DLL に*hconnection*パラメーターを介してこのハンドルが渡されます。  
[Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)または[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV ハンドラー関数が呼び出された後に、Extensions DLL が IHV 拡張関数を呼び出すことはできません。
- **関連付け後に呼び出されます。**  
IHV 機能拡張関数は、基本サービスセット (BSS) ネットワークでアソシエーション後操作を開始するために[Dot11ExtIhvPerformPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV ハンドラー関数が呼び出された後にのみ呼び出すことができます。  
IHV 拡張関数には、BSS ネットワーク接続とのセキュリティセッションを識別するハンドルが必要です。 *Dot11ExtIhvPerformPostAssociate*が呼び出されると、IHV 拡張 DLL は*hsecuritysessionid*パラメーターを介してこのハンドルに渡されます。  
[Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)または[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV ハンドラー関数が呼び出された後に、Extensions DLL が IHV 拡張関数を呼び出すことはできません。

| 関数 | サービスの初期化後に呼び出されます。 | アダプターの初期化後に呼び出されます。 | 事前関連付けの後に呼び出されます。 | 関連付け後に呼び出されます。 |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer) | X |   |   |   |
| [Dot11ExtFreeBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_free_buffer) | X |   |   |   |
| [Dot11ExtGetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data) |   |   | X |   | 
| [Dot11ExtNicSpecificExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) |   | X |   |   |
| [Dot11ExtStartOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start) |   |   |   | X |
| [Dot11ExtStopOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_stop) |   |   |   | X |
| [Dot11ExtPostAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) |   |   |   | X |
| [Dot11ExtPreAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) |   |   | X |   |
| [Dot11ExtProcessOneXPacket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet) |   |   |   | X |
| [Dot11ExtQueryVirtualStationProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties) |   | X |   |   |
| [Dot11ExtReleaseVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_release_virtual_station) |   | X |   |   |
| [Dot11ExtRequestVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station) |   | X |   |   |
| [Dot11ExtSendNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification) |   | X |   |   |
| [Dot11ExtSendUIRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) |   | X |   |   |
| [Dot11ExtSetAuthAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm) |   | X |   |   |
| [Dot11ExtSetCurrentProfile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_current_profile) |   |   | X |   |
| [Dot11ExtSetDefaultKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key) |   | X |   |   |
| [Dot11ExtSetDefaultKeyId](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)|   | X |   |   |
| [Dot11ExtSetEtherTypeHandling](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) |   | X |   |   |
| [Dot11ExtSetExcludeUnencrypted](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) |   | X |   |   |
| [Dot11ExtSetKeyMappingKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key) |   | X |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data) |   | X |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetVirtualStationAPProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties) |   |   | X |   | 

IHV ハンドラー関数の詳細については、「[ネイティブ 802.11 Ihv ハンドラー関数](native-802-11-ihv-handler-functions.md)」を参照してください。


