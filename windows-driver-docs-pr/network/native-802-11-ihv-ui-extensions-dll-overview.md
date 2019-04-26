---
title: ネイティブ 802.11 IHV UI 拡張 DLL の概要
description: ネイティブ 802.11 IHV UI 拡張 DLL の概要
ms.assetid: 82276ffb-eec4-4a77-9feb-f8f2ca1d7b34
keywords:
- DLL の IHV UI 拡張機能の拡張 DLL WDK ネイティブの 802.11 IHV UI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bcd8157f00cff341cecc4365a40af20ecd7c67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344236"
---
# <a name="native-80211-ihv-ui-extensions-dll-overview"></a>ネイティブ 802.11 IHV UI 拡張 DLL の概要




 

独立系ハードウェア ベンダー (IHV) は、ネイティブの 802.11 IHV 拡張機能の DLL を提供する場合、IHV は、802.11 IHV UI 拡張機能のネイティブの DLL を必要に応じて指定できます。 この DLL を IHV は、次の操作を行うことができます。

-   Microsoft ネットワーク構成ユーザー インターフェイス (UI) プロパティは、ワイヤレス接続とセキュリティの構成設定の使用を拡張します。 このような状況で 802.11 IHV UI 拡張機能のネイティブ DLL を次に操作できます。

    -   Microsoft 802.11 の標準プロパティには、カスタムの表示要素を追加します。 たとえば、802.11 IHV UI 拡張機能のネイティブ DLL では、独自のセキュリティ オプションの選択内容をエンドユーザーに提供するためのリストに項目を追加できます。
    -   独自の接続とセキュリティ設定を構成に使用できるカスタム UI を起動します。

    Microsoft の 802.11 プロパティの拡張の詳細については、次を参照してください。 [801.11 プロパティの拡張](extending-the-properties-for-wireless-network-profiles.md)します。

-   ネイティブの 802.11 IHV 拡張 DLL の要求時にカスタム UI を起動します。 基になるネイティブ 802.11 ミニポート ドライバーの現在の状態に応じて、オペレーティング システムとして、次のいずれかの UI が表示されます。

    -   オペレーティング システムの 802.11 UI のフロー内のウィザード ページのセット。 たとえば、ネイティブの 802.11 IHV 拡張 DLL は、ワイヤレス LAN (WLAN) 接続の操作中にユーザーの資格情報を必要とする場合、オペレーティング システム標準 UI フローの一部として、ネイティブの 802.11 UI 拡張機能の DLL によって提供されるカスタム UI ページが表示されます。

        バルーン通知から起動されたスタンドアロンの UI。 たとえば、ネイティブの 802.11 拡張 DLL が WLAN 接続で接続または認証の状態に変更を決定しますと、DLL が、802.11 UI 拡張機能のネイティブ DLL がエンドユーザーのアラートを生成するバルーン通知を表示要求できます。

    ネイティブの 802.11 拡張 DLL からの要求に起因する UI を起動する詳細については、次を参照してください。 [802.11 IHV 拡張 dll のネイティブ UI の要求を処理](handling-requests-for-the-display-of-a-custom-ui.md)します。

ネイティブの 802.11 IHV 拡張 DLL の詳細については、次を参照してください。 [802.11 IHV 拡張機能のネイティブの DLL](native-802-11-ihv-extensions-dll4.md)します。

Microsoft ネットワークの構成 UI やその他のネイティブの 802.11 コンポーネントに関する詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

 

 





