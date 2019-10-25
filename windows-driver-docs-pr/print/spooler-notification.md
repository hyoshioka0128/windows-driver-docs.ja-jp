---
title: スプーラ通知
description: スプーラ通知
ms.assetid: b5d9b909-f2e4-4773-903e-1dd73b0ca567
keywords:
- スプーラ通知 WDK 印刷
- 印刷スプーラの通知 WDK
- 通知 WDK 印刷スプーラ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dfa8a4aea7b8143a0372a4fc9efb5b34d1da044
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840403"
---
# <a name="spooler-notification"></a>スプーラ通知





この機能は、Windows Vista 以降で使用できます。

スプーラ通知メカニズムは、スプーラホストコンポーネント (プリンタードライバー、プリントプロセッサ、ポートモニターなど) とアプリケーションの間で双方向の通信パスを提供します。 関連するアプリケーションは、さまざまなセッションとセキュリティコンテキストで実行できます。

スプーラ通知メカニズムは、スプーラプロセスで実行される印刷コンポーネントが、印刷ジョブが開始されたセッションのユーザーインターフェイス要素を表示する必要がある場合に発生する問題を解決します。 Windows 2000 以前では、これらの印刷コンポーネントによって表示されるすべての UI は、セッション 0 (スプーラサービスが実行されるセッション) に常に表示されます。 この問題に対処するために、Windows XP、 [**SplPromptUIInUsersSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splpromptuiinuserssession) 、およびの2つのスプーラ関数が追加[**されまし**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splissessionzero)た。 スプーラ通知メカニズムには、これらの機能よりも多くの機能が用意されています。これらの機能は、ダイアログボックスでのメッセージの表示に限定されています。

[スプーラ通知の概要](overview-of-spooler-notification.md)

[スプーラの通知に関する用語](spooler-notification-terminology.md)

[パブリックインターフェイス](public-interfaces.md)

 

 




