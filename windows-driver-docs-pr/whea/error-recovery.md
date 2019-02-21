---
title: エラーからの回復
description: エラーからの回復
ms.assetid: 5710625f-bb65-41d4-a5c9-d61a48178859
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーからの回復
- WHEA WDK、エラーからの回復
- ハードウェア エラー WDK WHEA、エラーからの回復
- エラー WDK WHEA、エラーからの回復
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーからの回復
- PSHED プラグイン WDK WHEA、エラーからの回復
- WDK WHEA エラーの回復
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19df39bf26e3bf061fb08d09a2e9d7b45d433e6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553255"
---
# <a name="error-recovery"></a>エラーからの回復


回復可能なハードウェア エラーの処理中に、オペレーティング システムは、エラー条件から回復しようとします。 まず、オペレーティング システムは、独自のエラー条件から回復しようとします。 Windows カーネルを呼び出して、エラー条件から回復するために必要なハードウェアの操作を実行する機会を提供するよう PSHED にします。 エラーからの回復に参加しているプラグイン PSHED が実装されている場合、呼び出されます、PSHED でエラー条件から完全に回復するには、必要なプラットフォーム固有のハードウェアの追加操作を実行できるようにします。 かどうか、オペレーティング システムは、独自のエラー条件から正常に回復に関係なく、Windows カーネル常に呼び出し、PSHED と、登録済みの PSHED プラグインの更新またはとしてハードウェアの状態を変更することであることを確認するよう PSHEDいる。

エラーからの回復に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラーからの回復に参加している](participating-in-error-recovery.md)します。

 

 




