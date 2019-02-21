---
title: 通知チャネルの両端で実装されるインターフェイス
description: 通知チャネルの両端で実装されるインターフェイス
ms.assetid: cc6f1b06-c185-4915-a212-d0b3a2702d5d
keywords:
- スプーラ通知 WDK の印刷、チャネル
- 印刷スプーラ通知 WDK とチャネル
- 通知チャネルの WDK 印刷スプーラー
- チャネル通知 WDK の印刷スプーラー
- データ チャネルの WDK スプーラーの通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf6e5128be561a2643635bfe428e9431a6f20b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535533"
---
# <a name="interfaces-implemented-at-both-ends-of-the-notification-channel"></a>通知チャネルの両端で実装されるインターフェイス





次の図は、スプーラーの非同期通知で使用する COM インターフェイスを示します。

![スプーラ非同期通知で使用されている com インターフェイスを示す図](images/splnotarch.png)

図の左側にあるは、スプーラーが実装するインターフェイスと、通知チャネルの側を示しています。 図の右側にあるは、アプリケーションまたは印刷コンポーネント、および、スプーラーのサーバー側で実装されるによって実装されるインターフェイスと共に、通知チャネルのリスナーの側を示しています。 送信者とリスナーは、破線の線の上に示されるインターフェイスを実装します。 スプーラは、インターフェイス、および破線の線の下に示す機能を実装します。

 

 




