---
title: ネイティブ 802.11 IHV 拡張 DLL の概要
description: ネイティブ 802.11 IHV 拡張 DLL の概要
ms.assetid: 6a3d3e62-41b3-4ae2-a379-273431a36bb1
keywords:
- ネイティブ 802.11 IHV 拡張 DLL の拡張 DLL WDK ネイティブの 802.11 IHV
- ネイティブの 802.11 IHV 拡張 DLL の詳細について、ネイティブの 802.11 IHV 拡張機能の DLL WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba96bc3507d8b2456031985755ce2246157c4fde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575000"
---
# <a name="native-80211-ihv-extensions-dll-overview"></a>ネイティブ 802.11 IHV 拡張 DLL の概要




 

IHV 拡張機能の DLL を使用、独立系ハードウェア ベンダー (IHV) は、次にサポートできます。

-   専用のまたは非標準の認証アルゴリズム。 このサポートは、IHV 拡張機能の DLL は送信し、認証アルゴリズムに関連するすべてのセキュリティ パケットを受信します。

    IHV 拡張機能の DLL では、オペレーティング システムでサポートされていないネットワーク構成の標準的な認証アルゴリズムもサポートできます。 たとえば、DLL サポートできます事前共有キー (WPA-PSK) 認証アルゴリズムで、Wi-fi Protected Access、独立系の基本的なサービスのセット (IBSS) ネットワークで Windows Vista でサポートされていない構成します。

-   専用のまたは非標準の暗号アルゴリズム。 このサポートを通して、IHV 拡張機能の DLL が暗号キーを派生させ、ネイティブの 802.11 ミニポート ドライバーにキーをダウンロード責任を負います。

    IHV 拡張機能の DLL では、オペレーティング システムでサポートされていないネットワーク構成の標準的な暗号アルゴリズムもサポートできます。 たとえば、DLL をサポートできますテンポラル Key Integrity Protocol (TKIP) IBSS のネットワーク経由で Windows Vista でサポートされていない構成であります。

-   ネットワーク プロファイルに専用の拡張機能を検証します。 たとえば、IHV 拡張機能の DLL は、IHV が定義したセキュリティ オプションのユーザー設定の検証を担当します。

-   ネイティブの 802.11 ミニポート ドライバーの構成。 たとえば、ミニポート ドライバーで接続操作を開始する前に、オペレーティング システムが呼び出す、 [ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV 拡張機能の DLL が実行できるように関数BSS ネットワークへの接続に関連する専用の拡張機能で、ドライバーを構成します。

-   IHV UI 拡張機能の DLL へのインターフェイスします。 このインターフェイスでは、IHV 拡張機能の DLL は、ユーザー入力や通知を要求できます。 IHV UI 拡張機能の DLL の詳細については、[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)を参照してください。

ネイティブ 802.11 IHV 機能拡張のホスト プロセスでは、最初の到着と DLL がインストールされているワイヤレス LAN (WLAN) アダプターの検出時にプロセス空間に IHV 拡張機能の DLL を読み込みます。 ネイティブの 802.11 IHV 拡張機能ホスト プロセスとネイティブの 802.11 フレームワークの詳細については、[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)を参照してください。

ネイティブの 802.11 IHV 拡張機能ホスト プロセスは、その IHV 拡張関数を使用して API を提供します。 この API を使って IHV 拡張機能の DLL は、ネイティブ 802.11 ミニポート ドライバーまたは IHV UI 拡張機能の DLL インターフェイスことができます。 IHV 拡張機能の詳細については、[802.11 IHV 拡張関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560609)を参照してください。

同様に、IHV 拡張機能の DLL は、その IHV ハンドラー関数を使用して API を提供します。 ネイティブの 802.11 IHV 拡張機能ホスト プロセスは、処理前または後の関連の操作を開始するなど、さまざまな操作のこの API を使用します。 IHV ハンドラー関数の詳細については、[802.11 IHV ハンドラー関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560627)を参照してください。

 

 





