---
title: スプーラ通知
description: スプーラ通知
ms.assetid: b5d9b909-f2e4-4773-903e-1dd73b0ca567
keywords:
- WDK 印刷スプーラーの通知
- 印刷スプーラ通知 WDK
- 通知 WDK の印刷スプーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc6d51ffd7700c2a836f6ae161897cfd5b27e5b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552565"
---
# <a name="spooler-notification"></a>スプーラ通知





この機能は、以降 Windows Vista で利用できます。

スプーラの通知メカニズムは、(プリンター ドライバー、プリント プロセッサは、ポート モニターなど) のスプーラーでホストされるコンポーネントとアプリケーション間の双方向の通信パスを提供します。 関連するアプリケーションは、別のセッションとセキュリティ コンテキストで実行できます。

スプーラの通知メカニズムは、スプーラーのプロセスで実行される印刷コンポーネントは、印刷ジョブが開始されたセッションでユーザー インターフェイス要素を表示する必要がある場合に発生する問題を解決します。 Windows 2000 以降では、セッション 0 では、スプーラー サービスを実行するセッションで印刷コンポーネントで常に表示される UI が表示されます。 Windows xp では、この問題のために、2 つのスプーラー関数が追加された[ **SplPromptUIInUsersSession** ](https://msdn.microsoft.com/library/windows/hardware/ff562679)と[ **SplIsSessionZero** ](https://msdn.microsoft.com/library/windows/hardware/ff562677). スプーラの通知メカニズムは、ダイアログ ボックスでメッセージを表示することに制限されていますが、これらの関数よりも多くの機能を提供します。

[スプーラの通知の概要](overview-of-spooler-notification.md)

[スプーラ通知の用語集](spooler-notification-terminology.md)

[パブリック インターフェイス](public-interfaces.md)

 

 




