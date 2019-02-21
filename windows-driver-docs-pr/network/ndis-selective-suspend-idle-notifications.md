---
title: 選択的 NDIS がアイドル状態の通知を中断します。
description: 選択的 NDIS がアイドル状態の通知を中断します。
ms.assetid: 958A2588-A847-4699-9906-95FB47CA1CDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e6759c3617c1bf5342bd3eae75e1df3baa16f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553815"
---
# <a name="ndis-selective-suspend-idle-notifications"></a>選択的 NDIS がアイドル状態の通知を中断します。


ミニポート ドライバーが有効にし、選択的 NDIS のサポートを登録、中断、NDIS が基になるネットワーク アダプターの I/O アクティビティを監視します。 NDIS ドライバーとアダプターがアイドル状態である NDIS 実行と判断した場合、セレクティブ サスペンド操作。 この操作では、アダプターを低電力状態に遷移することによって、ネットワーク アダプターが中断します。

NDIS 開始、セレクティブ サスペンド操作ミニポート ドライバーにアイドル状態の通知を発行しています。 低電力状態で、ネットワーク アダプターが中断されると、アダプターは、アイドル状態の通知が取り消された場合にのみ電力状態に再開できます。 セレクティブ サスペンド操作後、通知は取り消され、アダプターが電力状態を完了します。

次のトピックで詳細を提供する選択的 NDIS 中断操作とアイドル状態の通知。

[NDIS がアイドル状態のネットワーク アダプターを検出する方法](how-ndis-detects-idle-network-adapters.md)

[アイドル状態の通知を中断する選択的 NDIS の処理](handling-the-ndis-selective-suspend-idle-notification.md)

[アイドル状態の通知を中断する選択的 NDIS のキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)

[アイドル状態の通知を中断する選択的 NDIS の完了](completing-the-ndis-selective-suspend-idle-notification.md)

 

 





