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
ms.openlocfilehash: 2f6fcbe43c6bce7fc63bbae4bed1cb7923851124
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575002"
---
# <a name="native-80211-ihv-extensibility-functions"></a>ネイティブの 802.11 IHV 拡張関数

> [!IMPORTANT]
> [ネイティブ 802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスが Windows 10 以降非推奨とされます。 代わりに、WLAN デバイス ドライバー インターフェイス (WDI) を使用してください。 WDI の詳細については、[WLAN のユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)を参照してください。

802.11 IHV のネイティブ機能拡張関数では、オペレーティング システムによって提供されは、次の操作を IHV 拡張機能の DLL によって呼び出されます。

- 割り当てし、ネイティブの 802.11 フレームワーク内で使用されるバッファーを解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを経由の認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- 任意の認証および IHV の拡張機能の DLL によってサポートされている暗号アルゴリズムのさまざまなセキュリティ設定、IHV の WLAN のアダプターを構成します。
- IHV UI 拡張 dll (インストールされている) 場合イベント通知を処理するインターフェイスします。 たとえば、IHV 拡張機能の DLL は、基本的なサービスのセット (BSS) ネットワーク接続に関連するさまざまな段階について IHV UI 拡張機能の DLL を通知できます。 

IHV UI 拡張機能の DLL の詳細については、[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)を参照してください。

> [!NOTE]
> IHV 拡張機能の DLL のメンバーに関連付けられている関数ポインターを通じて各ネイティブ 802.11 IHV 拡張関数を呼び出し、 [DOT11EXT_APIS](https://msdn.microsoft.com/library/windows/hardware/ff547617)構造体。 オペレーティング システムを呼び出すと、 [Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470) IHV ハンドラー関数を使用して、IHV 拡張関数をポインターのリストを渡しますが、 *pDot11ExtAPI*パラメーター。
 
IHV 拡張機能の DLL によって呼び出すことができるネイティブ 802.11 IHV 拡張関数を次の表に示します。 IHV 機能拡張の各関数は、これらの条件下でのみ呼び出すことができます。


- **サービスの初期化後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470) IHV 拡張機能の DLL を初期化するために、IHV ハンドラー関数が呼び出されました。 また、拡張 DLL が後 IHV 拡張関数を呼び出すことはできません、 [Dot11ExtIhvDeinitService](https://msdn.microsoft.com/library/windows/hardware/ff547457) IHV ハンドラー関数が呼び出されました。
- **アダプターの初期化後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvInitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547469) IHV ハンドラー関数が呼び出されて、IHV の WLAN のアダプター インターフェイスを初期化します。  
IHV 拡張関数では、WLAN アダプターを識別するハンドルが必要です。 ときに*Dot11ExtIhvInitAdapter*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hDot11SvcHandle*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452) IHV ハンドラー関数が呼び出されました。
- **関連付け前後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvPerformPreAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV ハンドラー関数が呼び出されて基本サービスのセット (BSS) ネットワークとの関連付け前操作を開始します。  
IHV 拡張関数では、BSS ネットワーク接続を識別するハンドルが必要です。 ときに*Dot11ExtIhvPerformPreAssociate*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hConnection*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)または[Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434) IHV ハンドラー関数が呼び出されています。
- **後のアソシエーションの後に呼び出されます**  
IHV 拡張関数は、後にのみ呼び出すことができます、 [Dot11ExtIhvPerformPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV ハンドラー関数が呼び出されて基本サービスのセット (BSS) ネットワークと後の関連付け操作を開始します。  
IHV 拡張関数では、BSS のネットワーク接続でセキュリティ セッションを識別するハンドルが必要です。 ときに*Dot11ExtIhvPerformPostAssociate*が呼び出されると、IHV 拡張機能の DLL を使ってこのハンドルを渡される、 *hSecuritySessionID*パラメーター。  
拡張 DLL は、IHV 拡張関数の後で呼び出すことはできません、 [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)または[Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434) IHV ハンドラー関数が呼び出されています。

| 関数 | サービスの初期化後に呼び出されます | アダプターの初期化後に呼び出されます | 関連付け前後に呼び出されます | 後のアソシエーションの後に呼び出されます |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](https://msdn.microsoft.com/library/windows/hardware/ff547419) | x |   |   |   |
| [Dot11ExtFreeBuffer](https://msdn.microsoft.com/library/windows/hardware/ff547422) | x |   |   |   |
| [Dot11ExtGetProfileCustomUserData](https://msdn.microsoft.com/library/windows/hardware/ff547430) |   |   | x |   | 
| [Dot11ExtNicSpecificExtension](https://msdn.microsoft.com/library/windows/hardware/ff547526) |   | x |   |   |
| [Dot11ExtStartOneX](https://msdn.microsoft.com/library/windows/hardware/ff547610) |   |   |   | x |
| [Dot11ExtStopOneX](https://msdn.microsoft.com/library/windows/hardware/ff547614) |   |   |   | x |
| [Dot11ExtPostAssociateCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547530) |   |   |   | x |
| [Dot11ExtPreAssociateCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547538) |   |   | x |   |
| [Dot11ExtProcessOneXPacket](https://msdn.microsoft.com/library/windows/hardware/ff547541) |   |   |   | x |
| [Dot11ExtQueryVirtualStationProperties](https://msdn.microsoft.com/library/windows/hardware/ff547544) |   | x |   |   |
| [Dot11ExtReleaseVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547549) |   | x |   |   |
| [Dot11ExtRequestVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547556) |   | x |   |   |
| [Dot11ExtSendNotification](https://msdn.microsoft.com/library/windows/hardware/ff547560) |   | x |   |   |
| [Dot11ExtSendUIRequest](https://msdn.microsoft.com/library/windows/hardware/ff547567) |   | x |   |   |
| [Dot11ExtSetAuthAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547571) |   | x |   |   |
| [Dot11ExtSetCurrentProfile](https://msdn.microsoft.com/library/windows/hardware/ff547574) |   |   | x |   |
| [Dot11ExtSetDefaultKey](https://msdn.microsoft.com/library/windows/hardware/ff547578) |   | x |   |   |
| [Dot11ExtSetDefaultKeyId](https://msdn.microsoft.com/library/windows/hardware/ff547584)|   | x |   |   |
| [Dot11ExtSetEtherTypeHandling](https://msdn.microsoft.com/library/windows/hardware/ff547587) |   | x |   |   |
| [Dot11ExtSetExcludeUnencrypted](https://msdn.microsoft.com/library/windows/hardware/ff547589) |   | x |   |   |
| [Dot11ExtSetKeyMappingKey](https://msdn.microsoft.com/library/windows/hardware/ff547597) |   | x |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547599) |   | x |   |   |
| [Dot11ExtSetProfileCustomUserData](https://msdn.microsoft.com/library/windows/hardware/ff547603) |   | x |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547606) |   | x |   |   |
| [Dot11ExtSetVirtualStationAPProperties](https://msdn.microsoft.com/library/windows/hardware/ff547609) |   |   | x |   | 

IHV ハンドラー関数の詳細については、[802.11 IHV ハンドラー関数をネイティブ](native-802-11-ihv-handler-functions.md)を参照してください。


