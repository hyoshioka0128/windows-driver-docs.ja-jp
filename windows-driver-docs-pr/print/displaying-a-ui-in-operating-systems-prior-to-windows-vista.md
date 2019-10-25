---
title: Windows Vista より前のオペレーティング システムで UI を表示する
description: Windows Vista より前のオペレーティング システムで UI を表示する
ms.assetid: de62310e-b10a-49b0-9bcc-b918318b2728
keywords:
- 印刷スプーラ WDK、Windows Vista 以前の UI 表示のカスタマイズ
- スプーラ WDK 印刷のカスタマイズ、Windows Vista 以前の UI 表示
- 印刷スプーラコンポーネントのカスタマイズ WDK、Windows Vista 以前の UI 表示
- 印刷コンポーネントの UI を表示する
- WDK 印刷を表示する UI
- ユーザーインターフェイス WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ec8fb3b84cfc9f18225767b75e7282b7b79d259
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838031"
---
# <a name="displaying-a-ui-in-operating-systems-prior-to-windows-vista"></a>Windows Vista より前のオペレーティング システムで UI を表示する





-   スプーラのプロセスで実行されているコンポーネントには UI を表示しません。

    スプーラは、高い特権を持つセキュリティレベルで実行されます。そのため、UI を表示すると、悪意のあるユーザーコードのリスクに対してスプーラが開かれます。

-   ドライバーのエラーを確認します。

    Windows Vista より前のオペレーティングシステムのリリースでは、非同期通知呼び出しが失敗します。

-   [**SplPromptUIInUsersSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splpromptuiinuserssession)関数を使用して、簡単なダイアログボックスを表示します。

-   ステータスモニターを作成して、複雑なユーザーインターフェイス要素を表示します。

    Status monitor は、IHV が開発し、ユーザーがインストールするアプリケーションです。 ステータスモニタはユーザーの資格情報に基づいてユーザーのコンテキストで実行されるため、ステータスモニタが UI 要素をいつでも表示するのは安全です。 Status monitor は、双方向通信または TCPMON Xcv インターフェイスを使用してスプーラと通信できます。 詳細については、「[双方向通信](adding-bidirectional-communication.md)と[Tcpmon Xcv インターフェイス](tcpmon-xcv-interface.md)の追加」を参照してください。

 

 




