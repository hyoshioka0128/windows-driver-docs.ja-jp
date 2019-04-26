---
title: CM_PROB_REGISTRY_TOO_LARGE
description: CM_PROB_REGISTRY_TOO_LARGE
ms.assetid: 8870ea57-4ae4-48a0-9d56-c5d0da8e1525
keywords:
- CM_PROB_REGISTRY_TOO_LARGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9609c78fbceb0712adbc9e723e5172d6663a87bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355726"
---
# <a name="cmprobregistrytoolarge"></a>CM_PROB_REGISTRY_TOO_LARGE

この関数は、システムの使用に予約されています。

レジストリが大きすぎます。

## <a name="error-code"></a>エラー コード

49

### <a name="display-message"></a>メッセージを表示します。

"システム ハイブが大きすぎるために、Windows が新しいハードウェア デバイスを起動できません (レジストリのサイズ制限を超える場合)。 (コード 49)"

### <a name="recommended-resolution"></a>推奨される解決方法

DEVMGR_SHOW_NONPRESENT_DEVICES 環境変数を 1 に設定します。 これによりが現在存在しない表示がインストールされているデバイスをデバイス マネージャーがさせます。 デバイス マネージャーを使用して、これらのデバイスを削除します。 レジストリが大きすぎて、Windows を再インストールします。
