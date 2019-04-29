---
title: NDIS セレクティブ サスペンド
description: NDIS セレクティブ サスペンド
ms.assetid: B0D44AE3-5197-4264-9838-83FB5EFEB0B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e487e400ccb97482ca7fa3adae88d03f20fc38f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387148"
---
# <a name="ndis-selective-suspend"></a>NDIS セレクティブ サスペンド


NDIS 6.30 以降では、選択的 NDIS 中断インターフェイスでは、アダプターを低電力状態に遷移することによって、アイドル状態のネットワーク アダプターを中断する NDIS できます。 これにより、CPU とネットワーク アダプターのオーバーヘッドが電力を減らすため、システムができます。

ここでは、次のトピックについて説明します。

[選択的 NDIS の概要を中断します。](overview-of-ndis-selective-suspend.md)

[レポートの NDIS 選択的な機能を中断します。](reporting-ndis-selective-suspend-capabilities.md)

[選択的登録 NDIS 中断ハンドラー関数](registering-ndis-selective-suspend-handler-functions.md)

[選択的 NDIS がアイドル状態の通知を中断します。](ndis-selective-suspend-idle-notifications.md)

[NDIS オプションを選択するための標準化された INF キーワードを中断します。](standardized-inf-keywords-for-ndis-selective-suspend.md)

[選択的 NDIS 中断実装ガイドライン](ndis-selective-suspend-implementation-guidelines.md)

**注**  インターフェイスは USB のネットワーク アダプターに特に便利です、インターフェイスがバスに依存しないが、選択的 NDIS を中断します。 その結果、ミニポート ドライバーでは、CPU を削減し、オーバーヘッドの電源をするために他のバスの種類のネットワーク アダプターのインターフェイスを使用することができます。

 

 

 





