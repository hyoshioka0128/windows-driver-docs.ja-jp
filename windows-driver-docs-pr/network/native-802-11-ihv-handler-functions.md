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
ms.openlocfilehash: 3c92d8407c06c5ab590d047f4378439f4c65c3a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528507"
---
# <a name="native-80211-ihv-handler-functions"></a>ネイティブの 802.11 IHV ハンドラー関数

>[!IMPORTANT]
> [ネイティブ 802.11 ワイヤレス LAN](native-802-11-wireless-lan4.md)インターフェイスが Windows 10 以降非推奨とされます。 代わりに、WLAN デバイス ドライバー インターフェイス (WDI) を使用してください。 WDI の詳細については、[WLAN のユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)を参照してください。

ネイティブの 802.11 IHV ハンドラー関数は、IHV 拡張機能の DLL によって提供されには、次のオペレーティング システムによって呼び出されます。

- 割り当てし、ネイティブの 802.11 フレームワーク内で使用されるバッファーを解放します。
- IHV のワイヤレス LAN (WLAN) アダプターを経由の認証アルゴリズムによって定義されたパケットなどのパケットを送信します。
- 指定された一連の IEEE EtherType 値とプライバシーの除外規則に基づいてパケットが表示されます。
- IHV の WLAN のアダプターを構成するには、独自の認証と暗号アルゴリズムのさまざまなセキュリティ設定。
- IHV UI 拡張 dll (インストールされている) 場合イベント通知を処理するインターフェイスします。 たとえば、IHV 拡張機能の DLL は、基本的なサービスのセット (BSS) ネットワーク接続に関連するさまざまな段階について UI 拡張機能の DLL を通知できます。 

IHV UI 拡張機能の DLL の詳細については、[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)を参照してください。

> [!NOTE]
> 例外として[Dot11ExtIhvGetVersionInfo](https://msdn.microsoft.com/library/windows/hardware/ff547464)と[Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470)、オペレーティング システムは、のメンバーに関連付けられている、関数ポインターを通じてIHVハンドラー関数を呼び出します。[DOT11EXT_IHV_HANDLERS](https://msdn.microsoft.com/library/windows/hardware/ff547625)構造体。 オペレーティング システムを呼び出すと、 *Dot11ExtIhvInitService* IHV ハンドラー関数で IHV 拡張機能の DLL を使用して、IHV ハンドラー関数をポインターのリストが返されます、 *pDot11IHVHandlers*パラメーター。

このセクションでは、次のネイティブの 802.11 IHV ハンドラー関数について説明します。

- [Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434)
- [Dot11ExtIhvControl](https://msdn.microsoft.com/library/windows/hardware/ff547438)
- [Dot11ExtIhvCreateDiscoveryProfiles](https://msdn.microsoft.com/library/windows/hardware/ff547445)
- [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)
- [Dot11ExtIhvDeinitService](https://msdn.microsoft.com/library/windows/hardware/ff547457)
- [Dot11ExtIhvGetVersionInfo](https://msdn.microsoft.com/library/windows/hardware/ff547464)
- [Dot11ExtIhvInitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547469)
- [Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470)
- [Dot11ExtIhvInitVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547475)
- [Dot11ExtIhvIsUIRequestPending](https://msdn.microsoft.com/library/windows/hardware/ff547479)
- [Dot11ExtIhvOneXIndicateResult](https://msdn.microsoft.com/library/windows/hardware/ff547482)
- [Dot11ExtIhvPerformCapabilityMatch](https://msdn.microsoft.com/library/windows/hardware/ff547488)
- [Dot11ExtIhvPerformPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547492)
- [Dot11ExtIhvPerformPreAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547499)
- [Dot11ExtIhvProcessSessionChange](https://msdn.microsoft.com/library/windows/hardware/ff547501)
- [Dot11ExtIhvProcessUIResponse](https://msdn.microsoft.com/library/windows/hardware/ff547504)
- [Dot11ExtIhvQueryUIRequest](https://msdn.microsoft.com/library/windows/hardware/ff547507)
- [Dot11ExtIhvReceiveIndication](https://msdn.microsoft.com/library/windows/hardware/ff547512)
- [Dot11ExtIhvReceivePacket](https://msdn.microsoft.com/library/windows/hardware/ff547513)
- [Dot11ExtIhvSendPacketCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547516)
- [Dot11ExtIhvStopPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547521)
- [Dot11ExtIhvValidateProfile](https://msdn.microsoft.com/library/windows/hardware/ff547523)

