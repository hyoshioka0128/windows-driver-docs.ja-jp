---
title: 電話サービスをサポートしている CoNDIS WAN 操作
description: 電話サービスをサポートしている CoNDIS WAN 操作
ms.assetid: 698d7667-8620-4f98-aa57-e48195f612e3
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワー キング、電話サービス
- WDK WAN 電話サービス
- ネットワーク NDPROXY WDK
- いる CoNDIS TAPI WDK ネットワーク
- 電話サービスの WDK WAN では、電話サービスです。
- WAN ミニポート ドライバー WDK ネットワー キング、電話サービス
- TAPI WDK のネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40eac07481ea4ba12824b8974c425556080508f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573994"
---
# <a name="condis-wan-operations-that-support-telephonic-services"></a>電話サービスをサポートしている CoNDIS WAN 操作





このセクションでは、いる CoNDIS WAN ミニポート ドライバーが接続指向の環境で NDIS 関数を使用する電話サービスを実装する方法について説明します。 いる CoNDIS WAN ミニポート ドライバーは、NDIS を通じて、NDPROXY と NDISWAN ドライバーと通信します。 NDPROXY ドライバーは、テレフォニー サービス プロバイダー経由のテレフォニー アプリケーションと通信します。 詳細については、テレフォニー アプリケーション プログラミング インターフェイス (TAPI)、Microsoft Windows SDK ドキュメントを参照してください。

次のトピックより完全 NDPROXY ドライバーを説明します。 これらのトピックについても説明しましている CoNDIS WAN ミニポート ドライバー登録機能、線を利用する方法設定する方法およびその TAPI を列挙および方法 TAPI 要求によって開始された呼び出しを閉じます。

[NDPROXY の概要](ndproxy-overview.md)

[いる CoNDIS TAPI の登録](condis-tapi-registration.md)

[いる CoNDIS TAPI の初期化](condis-tapi-initialization.md)

[発信呼び出しを行う](making-outgoing-calls.md)

[着信呼び出しの受け入れ](accepting-incoming-calls.md)

[いる CoNDIS TAPI シャット ダウン](condis-tapi-shutdown.md)

[音声のストリーミングにマネージャーの要件を呼び出す](call-manager-requirements-for-voice-streaming.md)

[接続指向の NDIS 経由で電話サービスをサポートする非 WAN 固有の拡張機能](non-wan-specific-extensions-to-support-telephonic-services-over-connec.md)

これらの説明では、TAPI に組み込まれている概念について簡単に説明が、リーダーは、詳細については、TAPI、Windows SDK を参照してください。 TAPI を方法についての詳細には、回線デバイスをモデル化し、すべて WAN ミニポート ドライバーでは、その接続の状態を維持する必要があります、方法を参照してください[回線デバイス、アドレス、および呼び出し (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549181)と[状態の維持。情報 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549232)します。

 

 





