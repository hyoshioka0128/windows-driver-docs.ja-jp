---
title: CM_PROB_REGISTRY_TOO_LARGE
description: CM_PROB_REGISTRY_TOO_LARGE
ms.assetid: 8870ea57-4ae4-48a0-9d56-c5d0da8e1525
keywords:
- CM_PROB_REGISTRY_TOO_LARGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ce2223c8144f0b8439bfefba4c04e7c8c1a4a4
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279495"
---
# <a name="code-49---cm_prob_registry_too_large"></a>コード 49-CM_PROB_REGISTRY_TOO_LARGE

このデバイスマネージャーエラーメッセージは、レジストリが大きすぎることを示します。

## <a name="error-code"></a>エラー コード

49

### <a name="display-message"></a>メッセージの表示

"システムハイブが大きすぎる (レジストリサイズの上限を超えている) ため、Windows は新しいハードウェアデバイスを起動できません。 (コード 49) "

### <a name="recommended-resolution"></a>推奨される解決策

環境変数 DEVMGR_SHOW_NONPRESENT_DEVICES を1に設定します。 これにより、現在存在していないインストール済みのデバイスがデバイスマネージャーに表示されます。 これらのデバイスを削除するには、デバイスマネージャーを使用します。 レジストリが大きすぎる場合は、Windows を再インストールしてください。
