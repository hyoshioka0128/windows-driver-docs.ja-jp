---
title: NDIS の選択的中断の概要
description: NDIS の選択的中断の概要
ms.assetid: B0D44AE3-5197-4264-9838-83FB5EFEB0B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e5d62e9a21e3c2de22121062a3e8e45f0c3f31a
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565662"
---
# <a name="introduction-to-ndis-selective-suspend"></a>NDIS の選択的中断の概要


Ndis 6.30 以降では、ndis の選択的中断インターフェイスを使用して、アダプターを低電力状態に移行することによって、NDIS でアイドル状態のネットワークアダプターを中断できます。 これにより、システムは CPU とネットワークアダプターの電力オーバーヘッドを軽減できます。

ここでは、次のトピックについて説明します。

[NDIS の選択的中断の概要](overview-of-ndis-selective-suspend.md)

[NDIS の選択的中断機能を報告する](reporting-ndis-selective-suspend-capabilities.md)

[NDIS の選択的中断ハンドラー関数を登録しています](registering-ndis-selective-suspend-handler-functions.md)

[NDIS の選択的中断のアイドル状態の通知](ndis-selective-suspend-idle-notifications.md)

[NDIS 選択的中断の標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NDIS 選択的中断実装ガイドライン](ndis-selective-suspend-implementation-guidelines.md)

**注:**   NDIS の選択的中断インターフェイスは、USB ネットワークアダプターに特に便利ですが、インターフェイスはバスに依存しません。 その結果、ミニポートドライバーは、CPU と電力のオーバーヘッドを減らすために、他の種類のバスのネットワークアダプターのインターフェイスを使用できます。

 

 

 





