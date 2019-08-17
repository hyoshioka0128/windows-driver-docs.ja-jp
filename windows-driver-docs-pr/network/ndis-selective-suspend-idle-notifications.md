---
title: NDIS セレクティブサスペンドアイドル通知の概要
description: NDIS セレクティブサスペンドアイドル通知の概要
ms.assetid: 958A2588-A847-4699-9906-95FB47CA1CDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ffc791350d572f62368134565e450f071ced315
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565645"
---
# <a name="overview-of-ndis-selective-suspend-idle-notifications"></a>NDIS セレクティブサスペンドアイドル通知の概要


ミニポートドライバーが有効になっていて、NDIS の選択的中断がサポートされている場合、NDIS は基になるネットワークアダプターの i/o アクティビティを監視します。 NDIS がドライバーとアダプターがアイドル状態であると判断した場合、NDIS はセレクティブサスペンド操作を実行します。 この操作では、アダプターを低電力状態に移行することで、ネットワークアダプターを中断します。

NDIS は、ミニポートドライバーにアイドル通知を発行することによって、セレクティブサスペンド操作を開始します。 ネットワークアダプターが低電力状態で中断されている場合、アダプターはアイドル状態の通知が取り消された場合にのみ、フルパワー状態に再開できます。 通知が取り消され、アダプターがフルパワー状態になると、セレクティブサスペンド操作が完了します。

次のトピックでは、NDIS のセレクティブサスペンド操作とアイドル状態の通知について詳しく説明します。

[NDIS がアイドル状態のネットワークアダプターを検出する方法](how-ndis-detects-idle-network-adapters.md)

[NDIS の選択的中断を待機する通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)

[NDIS の選択的中断のアイドル通知をキャンセルしています](canceling-the-ndis-selective-suspend-idle-notification.md)

[NDIS の選択的中断のアイドル通知を完了しています](completing-the-ndis-selective-suspend-idle-notification.md)

 

 





