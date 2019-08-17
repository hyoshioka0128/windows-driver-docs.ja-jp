---
title: ミニポートアダプターの開始と一時停止の概要
description: ミニポートアダプターの開始と一時停止の概要
ms.assetid: d278b331-90d9-4d19-bf00-732981962522
keywords:
- ミニポートアダプター WDK ネットワーク、開始
- WDK ネットワークのアダプター、開始
- ミニポートアダプター WDK ネットワーク、一時停止
- WDK ネットワークのアダプター、一時停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46dbbb373a15d1defa6cab7341fcc18f5d55888e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565740"
---
# <a name="starting-and-pausing-a-miniport-adapter-overview"></a>ミニポートアダプターの開始と一時停止の概要





NDIS は、アダプターを一時停止して、フィルタードライバーの追加や削除などのプラグアンドプレイ操作や、NIC でのパケットフィルターやマルチキャストアドレス一覧の設定などの要求を妨げる可能性のあるデータフローを停止します。 実行中のドライバースタックを変更する方法の詳細については、「[実行中のドライバースタックの変更](modifying-a-running-driver-stack.md)」を参照してください。

NDIS は、アダプターを一時停止状態から再開します。 アダプターの初期化が完了した後、または一時停止操作が完了した後に、アダプターは一時停止した開始を入力します。

次のトピックでは、開始と一時停止およびアダプターの詳細について説明します。

-   [アダプターを開始する](starting-an-adapter.md)
-   [アダプターの一時停止](pausing-an-adapter.md)

 

 





