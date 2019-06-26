---
title: 双方向通信
description: 双方向通信
ms.assetid: c88f5f43-4a14-4f63-9f17-b6680fc0d645
keywords:
- プリンター構成 WDK、双方向通信
- 双方向通信 WDK の印刷
- 双方向通信 WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7c9e74f958032e052a242bcd7e0c63ca1f8c6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382583"
---
# <a name="bidirectional-communication"></a>双方向通信


印刷サブシステムとプリンターの間の双方向プリンター通信 (双方向の通信とも呼ばれます) は、プリンターの自動構成に不可欠です。 この通信は、Windows XP では、以降、Windows オペレーティング システムが付属して有効にドライバーとアプリケーションを要求を行うし、プリンター デバイスからの応答を取得します。 双方向通信に基づく自動構成とユーザーはアプリケーションが自分でプリンターを構成するための手段があるため、手動でインストール可能なオプションを選択ありません。

双方向通信のサポートには、2 つの部分が含まれます。

-   双方向の通信インターフェイスは、スプーラー Api の構成

-   双方向通信のスキーマ、デバイスと情報を交換するための標準的な XML

スキーマでは、アプリケーションがデバイスと、要求の形式に加えることが要求について説明します。 スプーラ Api デバイスへの要求の送信も送受信双方向データ。 アプリケーションは要求をネットワーク プリンターまたはリモート プリンター サーバーに接続されているプリンターをネットワーク印刷プロバイダーに送信もできます。

印刷スプーラが双方向通信をサポートする方法については、次を参照してください。[双方向通信の追加](adding-bidirectional-communication.md)と[スプーラー通知](spooler-notification.md)します。

## <a name="in-this-section"></a>このセクションの内容


[双方向通信のスキーマ](bidirectional-communication-schema.md)

## <a name="related-sections"></a>関連項目


[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)

[双方向通信のスキーマ参照](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)

[双方向通信のエラー コード](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-error-codes)

 

 




