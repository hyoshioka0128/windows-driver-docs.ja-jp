---
title: CM_PROB_DUPLICATE_DEVICE
description: CM_PROB_DUPLICATE_DEVICE
ms.assetid: db0f6c98-d314-4882-ac8e-c73254f41c98
keywords:
- CM_PROB_DUPLICATE_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d66f1ec6fec173426c2867d00374bb70f16c2f59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385626"
---
# <a name="cmprobduplicatedevice"></a>CM_PROB_DUPLICATE_DEVICE

この関数は、システムの使用に予約されています。

重複するデバイスが検出されました。

## <a name="error-code"></a>エラー コード

42

### <a name="display-message"></a>メッセージを表示します。

"Windows 読み込むことができませんこのハードウェアのデバイス ドライバー、システムで既に実行されている重複するデバイスがあるためです。 (コード 42)"

### <a name="recommended-resolution"></a>推奨される解決方法

次のいずれかが発生した場合、このエラーが報告されます。

- オペレーティング システムが古い場所から、デバイスが見つからないことを通知する前に、コンピューターに新しい場所にシリアル番号を持つデバイスが検出されます。 これは、デバイスが移動非常に短時間である場合、またはコンピューターが、スタンバイ状態または休止状態は、別の場所に通常発生します。

    この場合、コンピューターを再起動して問題が解決することができます。

- バス ドライバーで作成、バスの 2 つの同じ名前を持つ子 これは、同じシリアル番号を報告するバス上の複数のデバイスが原因です。 2 つまたは複数のデバイスの同じハードウェア識別子を正しく報告するバス ドライバーが原因の可能性もあります。

    ここでお問い合わせください[Microsoft サポート](https://support.microsoft.com/en-us)にこの問題に問い合わせます。
