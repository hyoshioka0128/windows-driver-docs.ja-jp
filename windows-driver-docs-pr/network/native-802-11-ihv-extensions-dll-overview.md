---
title: ネイティブ 802.11 IHV 拡張 DLL の概要
description: ネイティブ 802.11 IHV 拡張 DLL の概要
ms.assetid: 6a3d3e62-41b3-4ae2-a379-273431a36bb1
keywords:
- IHV 拡張 DLL WDK ネイティブ802.11、ネイティブ 802.11 IHV 拡張 DLL について
- ネイティブ 802.11 IHV 拡張 DLL WDK、ネイティブ 802.11 IHV 拡張 DLL について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab4d37698552b7c243fbed962fef1f429ef85e8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839641"
---
# <a name="native-80211-ihv-extensions-dll-overview"></a>ネイティブ 802.11 IHV 拡張 DLL の概要




 

IHV 拡張 DLL を使用すると、独立系ハードウェアベンダー (IHV) は次のことをサポートできます。

-   専用または非標準の認証アルゴリズム。 このサポートにより、IHV 拡張 DLL は、認証アルゴリズムに関連するすべてのセキュリティパケットを送受信します。

    また、IHV 拡張 DLL では、オペレーティングシステムでサポートされていないネットワーク構成の標準的な認証アルゴリズムもサポートできます。 たとえば、DLL は、Windows Vista でサポートされていない構成である独立した基本サービスセット (IBSS) ネットワークに対する、事前共有キー (WPA-PSK) 認証アルゴリズムを使用した Wi-fi 保護アクセスをサポートできます。

-   専用または非標準の暗号アルゴリズム。 このサポートにより、IHV 拡張 DLL は、暗号キーを派生させ、キーをネイティブ802.11 ミニポートドライバーにダウンロードします。

    また、IHV 拡張 DLL では、オペレーティングシステムでサポートされていないネットワーク構成の標準暗号アルゴリズムをサポートすることもできます。 たとえば、DLL は、Windows Vista ではサポートされていない構成である IBSS ネットワーク経由のテンポラルキー整合性プロトコル (TKIP) をサポートできます。

-   ネットワークプロファイルに対する独自の拡張機能の検証。 たとえば、ihv 拡張 DLL は、IHV が定義したセキュリティオプションのユーザー設定の検証を担当します。

-   ネイティブ802.11 ミニポートドライバーの構成。 たとえば、ミニポートドライバーを使用して接続操作を開始する前に、オペレーティングシステムは[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数を呼び出します。これにより、IHV 拡張 DLL は、に関連する独自の拡張機能を使用してドライバーを構成できます。BSS ネットワークへの接続。

-   IHV UI 拡張 DLL へのインターフェイス。 このインターフェイスを使用して、IHV 拡張 DLL はユーザーの入力または通知を要求できます。 IHV UI 拡張 DLL の詳細については、「[ネイティブ 802.11 IHV Ui EXTENSIONS dll](native-802-11-ihv-ui-extensions-dll2.md)」を参照してください。

ネイティブ 802.11 IHV 拡張ホストプロセスは、DLL がインストールされているワイヤレス LAN (WLAN) アダプターの初回到着時および検出時に、そのプロセス領域に IHV 拡張 DLL を読み込みます。 ネイティブ 802.11 IHV 拡張ホストプロセスとネイティブ802.11 フレームワークの詳細については、「[ネイティブ802.11 ソフトウェアアーキテクチャ](native-802-11-software-architecture.md)」を参照してください。

ネイティブ 802.11 IHV 拡張ホストプロセスでは、IHV 拡張機能を介して API を提供します。 この API を使用して、IHV 拡張 DLL はネイティブ802.11 ミニポートドライバーまたは IHV UI 拡張 DLL をインターフェイスできます。 IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

同様に、IHV 拡張 DLL は、IHV ハンドラー関数を介して API を提供します。 ネイティブ 802.11 IHV 拡張ホストプロセスでは、この API を使用して、または関連付け後の操作を開始するなど、さまざまな操作を行います。 IHV ハンドラー関数の詳細については、「[ネイティブ 802.11 Ihv ハンドラー関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)」を参照してください。

 

 





