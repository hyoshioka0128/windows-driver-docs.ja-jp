---
title: CM_PROB_FAILED_DRIVER_ENTRY
description: CM_PROB_FAILED_DRIVER_ENTRY
ms.assetid: e1345892-69db-4135-be5b-1d182a2a1d66
keywords:
- CM_PROB_FAILED_DRIVER_ENTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40198115ad0c807836b3fb33c7d142923144bdd6
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279569"
---
# <a name="code-37---cm_prob_failed_driver_entry"></a>コード 37-CM_PROB_FAILED_DRIVER_ENTRY

このデバイスマネージャーエラーメッセージは、ドライバーが**Driverentry**ルーチンからエラーを返したことを示します。

## <a name="error-code"></a>エラー コード

37

### <a name="display-message"></a>メッセージの表示

"このハードウェアのデバイスドライバーを初期化できません。 (コード 37) "

### <a name="recommended-resolution"></a>推奨される解決策

新しいドライバを再インストールまたは取得します。

**Driverentry**ルーチンが STATUS_INSUFFICIENT_RESOURCES を返した場合、デバイスマネージャーは[CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)エラーコードを**報告  ます**。
