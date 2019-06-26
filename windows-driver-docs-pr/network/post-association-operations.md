---
title: 関連付け後の操作
description: 関連付け後の操作
ms.assetid: e4c7ea7a-53ad-41b2-bf3f-03c770e58043
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、後の関連付け操作
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- ネイティブ 802.11 IHV 拡張 DLL WDK、後の関連付け操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1d8ffc5cee77d066707170965fbc23464c76856
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384533"
---
# <a name="post-association-operations"></a>関連付け後の操作




 

ワイヤレス LAN (WLAN) アダプターには、アクセス ポイント (AP) の関連付け操作は正常に完了すると、オペレーティング システムは、アソシエーションのデータ ポートを作成します。 オペレーティング システムを呼び出してデータ ポートでの後の関連付け操作を開始します、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数。

**注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

 

後の関連付け操作を実行するときに、IHV 拡張 DLL は、以下を実行できます。

-   新しいデータ ポートに必要なすべてのリソースを割り当てます。

-   独自のセキュリティがデータ ポートの関連付け前の操作中に構成された認証アルゴリズムのためにパケットを送受信することなどの処理を実行します。 この操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   暗号キーを派生し、WLAN アダプターにダウンロードします。

オペレーティング システムが呼び出すことによってデータ ポートで、後の関連付け操作を終了する WLAN アダプターでは、AP との関連付け解除操作が完了したら、 [ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数。 この呼び出しでは、次のオペレーティング システムは、アソシエーションのデータ ポートを削除します。

次のトピックでは、後の関連付け操作を停止または実行を行う必要があります IHV 拡張機能の DLL について説明します。

[後の関連付け操作を実行します。](performing-a-post-association-operation.md)

[後の関連付け操作を停止します。](stopping-a-post-association-operation.md)

[インターフェイスをネイティブの 802.11 802.1 X モジュール](interface-to-the-native-802-11-802-1x-module.md)

関連付け操作の詳細については、次を参照してください。[関連付け操作](association-operations.md)します。

関連付け解除操作の詳細については、次を参照してください。[関連付け解除操作](disassociation-operations.md)します。

ポートの管理に関連する手順の詳細については、次を参照してください。[ポート ベースのネットワーク アクセス](port-based-network-access.md)します。

 

 





