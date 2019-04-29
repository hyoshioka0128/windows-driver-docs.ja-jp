---
title: ミニポート アダプターの起動と一時停止
description: ミニポート アダプターの起動と一時停止
ms.assetid: d278b331-90d9-4d19-bf00-732981962522
keywords:
- ミニポート アダプタの WDK ネットワーク、開始
- アダプターの WDK ネットワーク、開始
- ミニポート アダプタ WDK ネットワーク、一時停止
- アダプター WDK ネットワーク、一時停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7cc9ef56c74eb8644c19128be1503737d942f76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390631"
---
# <a name="starting-and-pausing-a-miniport-adapter"></a>ミニポート アダプターの起動と一時停止





NDIS は、フィルター ドライバー、または NIC のパケット フィルターまたはマルチキャスト アドレスの一覧の設定などの要求は、追加または削除などのプラグ アンド プレイ操作を妨げる可能性があるデータ フローを終了するためのアダプターを一時停止します。 実行中のドライバー スタックを変更する方法の詳細については、次を参照してください。[変更を実行しているドライバー スタック](modifying-a-running-driver-stack.md)します。

NDIS は、一時停止状態からアダプターを再起動します。 アダプターの初期化が完了した後、または一時停止操作が完了した後、アダプターは一時停止の開始を入力します。

開始、一時停止およびアダプターの詳細については、以下のトピックです。

-   [アダプターの開始](starting-an-adapter.md)
-   [アダプターを一時停止](pausing-an-adapter.md)

 

 





