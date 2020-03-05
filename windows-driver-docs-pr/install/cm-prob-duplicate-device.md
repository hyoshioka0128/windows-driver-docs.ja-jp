---
title: CM_PROB_DUPLICATE_DEVICE
description: CM_PROB_DUPLICATE_DEVICE
ms.assetid: db0f6c98-d314-4882-ac8e-c73254f41c98
keywords:
- CM_PROB_DUPLICATE_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fe56dae488b031510d515b0c3754b456cb7335
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279577"
---
# <a name="code-42---cm_prob_duplicate_device"></a>コード 42-CM_PROB_DUPLICATE_DEVICE

このデバイスマネージャーエラーメッセージは、重複するデバイスが検出されたことを示します。

## <a name="error-code"></a>エラー コード

42

### <a name="display-message"></a>メッセージの表示

"システムで既に実行されている重複するデバイスがあるため、Windows はこのハードウェアのデバイスドライバーを読み込めません。 (コード 42) "

### <a name="recommended-resolution"></a>推奨される解決策

このエラーは、次のいずれかが発生した場合に報告されます。

- コンピューター内の新しい場所でシリアル番号を持つデバイスが検出されると、デバイスが古い場所から失われていることがオペレーティングシステムから通知されます。 これは通常、デバイスが移動されたときに、すぐに、またはコンピューターがスタンバイ状態または休止状態のときに、別の場所に移動したときに発生します。

    この場合、コンピューターを再起動することで問題を解決できます。

- バスドライバーでは、バス上に同じ名前の2つの同じ子が誤って作成されます。 これは、同じシリアル番号を報告するバス上の複数のデバイスによって発生します。 この問題は、2つ以上のデバイスに対して同じハードウェア識別子が誤って報告されるバスドライバーによって発生することもあります。

    この場合、この問題の詳細については、 [Microsoft サポート](https://support.microsoft.com/en-us)にお問い合わせください。
