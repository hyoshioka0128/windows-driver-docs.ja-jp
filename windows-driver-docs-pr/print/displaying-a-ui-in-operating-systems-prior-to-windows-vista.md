---
title: Windows Vista より前のオペレーティング システムで UI を表示する
description: Windows Vista より前のオペレーティング システムで UI を表示する
ms.assetid: de62310e-b10a-49b0-9bcc-b918318b2728
keywords:
- 印刷スプーラー WDK、以前の Windows Vista の UI の表示をカスタマイズします。
- スプーラ WDK の印刷、以前の Windows Vista の UI の表示のカスタマイズ
- 印刷スプーラー コンポーネント WDK、以前の Windows Vista の UI の表示のカスタマイズ
- 印刷コンポーネントの UI を表示します。
- UI 表示 WDK 印刷
- WDK の印刷のユーザー インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5991b4d50afaa2e30167076d9c719c749fa7f272
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364004"
---
# <a name="displaying-a-ui-in-operating-systems-prior-to-windows-vista"></a>Windows Vista より前のオペレーティング システムで UI を表示する





-   スプーラーのプロセスで実行されるすべてのコンポーネントでは、UI を表示しません。

    スプーラが、高い特権のセキュリティ レベルで実行します。そのため、UI を表示するには、悪意のあるユーザー コードのリスクにスプーラーが表示されます。

-   ドライバーでエラーを確認します。

    非同期通知の呼び出しは、Windows Vista より前のオペレーティング システムのリリースでは失敗します。

-   使用して単純なダイアログ ボックスを表示、 [ **SplPromptUIInUsersSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-splpromptuiinuserssession)関数。

-   状態の監視を記述することで、複雑なユーザー インターフェイス要素を表示します。

    状態の監視は、IHV が開発していると、ユーザーがインストールされるアプリケーションです。 Status monitor は、ユーザーの資格情報で、ユーザーのコンテキストで実行される、ためには、いつでも UI 要素を表示する状態モニタのも安全です。 Status monitor は、双方向通信を使用して、または TCPMON Xcv インターフェイスを使用して、スプーラーと通信できます。 詳しくは、次を参照してください。[双方向通信の追加](adding-bidirectional-communication.md)と[TCPMON Xcv インターフェイス](tcpmon-xcv-interface.md)します。

 

 




