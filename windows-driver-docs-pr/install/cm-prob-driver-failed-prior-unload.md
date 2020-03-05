---
title: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
description: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.assetid: c7639fd7-738f-4115-9abc-0bafca097b9e
keywords:
- CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d03c0461ce5abeb9c8e2cdbb33226562d3b071
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279581"
---
# <a name="code-38---cm_prob_driver_failed_prior_unload"></a>コード 38-CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD

このデバイスマネージャーエラーメッセージは、前のインスタンスがまだ読み込まれているためにドライバーを読み込めなかったことを示します。

## <a name="error-code"></a>エラー コード

38

### <a name="display-message"></a>メッセージの表示

"デバイスドライバの以前のインスタンスがまだメモリ内にあるため、このハードウェアのデバイスドライバを読み込めません。 (コード 38) "

### <a name="recommended-resolution"></a>推奨される解決策

以前のドライバーインスタンスは、参照カウントが正しくないか、読み込み操作とアンロード操作の間に競合が発生したため、引き続き読み込むことができます。 また、1つまたは複数の INF ファイル内の複数の[**Inf AddService ディレクティブ**](inf-addservice-directive.md)によってドライバーが参照されている場合にも、このメッセージが表示されることがあります。

**[コンピューターの再起動]** を選択すると、コンピューターが再起動されます。
