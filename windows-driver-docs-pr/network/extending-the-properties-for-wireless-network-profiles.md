---
title: ワイヤレス ネットワーク プロファイルのプロパティを拡張します。
description: ワイヤレス ネットワーク プロファイルのプロパティを拡張します。
ms.assetid: c98266b5-3841-4dfa-b274-5c1ef16bfef6
keywords:
- IHV UI 拡張 DLL WDK ネイティブ 802.11、ネットワーク プロファイルの拡張機能
- ネットワーク プロファイル WDK ネイティブ 802.11 IHV UI 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e053ab00c146956b6e66f347ae4b8228c3ebc0ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557521"
---
# <a name="extending-the-properties-for-wireless-network-profiles"></a>ワイヤレス ネットワーク プロファイルのプロパティを拡張します。




 

エンド ユーザーを作成または 802.11 ネットワークの構成をネイティブ ユーザー インターフェイス (UI) を介してワイヤレス ネットワーク接続プロファイルを編集します。 この UI の詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

独立系ハードウェア ベンダー (IHV) は、ネイティブの 802.11 UI 拡張機能の DLL を独自の接続とセキュリティ プロファイルの設定をサポートするためにネットワークの構成 UI を拡張できます。 DLL は、ネットワークの構成 UI に表示される次のタブに拡張できます。

<a href="" id="connection-tab"></a>**[接続] タブ**  
このタブには、ワイヤレス LAN (WLAN) のネットワークの接続設定の UI が表示されます。

802.11 IHV UI 拡張機能のネイティブ DLL で説明されている手順を実行してこの UI を拡張できます[ワイヤレス接続のプロパティ ページを拡張する](extending-wireless-connection-properties.md)します。

**注**  の Windows Vista では、802.11 UI 拡張機能のネイティブ DLL のみをサポートする 1 つの拡張機能、**接続**タブ。

 

<a href="" id="security-tab-------"></a>**[セキュリティ] タブ**   
このタブには、ワイヤレス LAN (WLAN) のネットワークのセキュリティ設定の UI が表示されます。

802.11 IHV UI 拡張機能のネイティブ DLL では、独自のセキュリティ設定の表示要素を追加することで、この UI を拡張できます。 このプロセスの詳細については、次を参照してください。[ワイヤレス セキュリティのプロパティ ページの拡張](extending-wireless-security-properties.md)します。

802.11 IHV UI 拡張機能のネイティブ DLL で、Microsoft 802.1 X 設定を拡張できますも、**セキュリティ**タブ。このプロセスの詳細については、次を参照してください。[を拡張する Microsoft 802.1 X のセキュリティ設定](extending-microsoft-802-1x-security-settings.md)します。

**注**  For Windows Vista 802.11 IHV UI 拡張機能のネイティブ DLL はインフラストラクチャ ワイヤレス ネットワーク用の接続およびセキュリティ プロファイルのプロパティを拡張してできるだけです。

 

 

 





