---
title: 双方向通信
description: 双方向通信
ms.assetid: c88f5f43-4a14-4f63-9f17-b6680fc0d645
keywords:
- プリンター構成 WDK、双方向通信
- 双方向通信の WDK 印刷
- bidi 通信 WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c9c77b84c77becbac881f8023d2cf6e061e4f7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841638"
---
# <a name="bidirectional-communication"></a>双方向通信


プリンターの自動構成には、印刷サブシステムとプリンターの双方向プリンター通信 (bidi 通信とも呼ばれます) が不可欠です。 Windows XP 以降の Windows オペレーティングシステムで提供されるこの通信により、ドライバーとアプリケーションはプリンターデバイスに対して要求を行い、応答を取得することができます。 双方向通信に基づく自動構成を使用する場合、ユーザーは手動でインストール可能なオプションを選択する必要はありません。これは、アプリケーションがプリンターを独自に構成する方法があるためです。

Bidi 通信のサポートには、次の2つの部分が含まれます。

-   スプーラ Api で構成される双方向通信インターフェイス

-   双方向通信スキーマ (デバイスと情報を交換するための XML 標準)

スキーマでは、アプリケーションがデバイスに対して実行できる要求と、要求の形式を記述します。 スプーラ Api は、デバイスに要求を送信し、bidi データも送受信します。 また、アプリケーションは、ネットワークプリンターまたはリモートプリンターサーバーに接続されているプリンターのネットワーク印刷プロバイダーに要求を送信することもできます。

印刷スプーラで双方向通信をサポートする方法の詳細については、「[双方向通信](adding-bidirectional-communication.md)と[スプーラ通知](spooler-notification.md)の追加」を参照してください。

## <a name="in-this-section"></a>このセクションの内容


[双方向通信スキーマ](bidirectional-communication-schema.md)

## <a name="related-sections"></a>関連セクション


[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)

[双方向通信スキーマリファレンス](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)

[双方向の通信エラーコード](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-error-codes)

 

 




