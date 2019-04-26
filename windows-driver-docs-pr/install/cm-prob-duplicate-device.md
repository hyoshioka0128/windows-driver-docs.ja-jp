---
title: CM_PROB_DUPLICATE_DEVICE
description: CM_PROB_DUPLICATE_DEVICE
ms.assetid: db0f6c98-d314-4882-ac8e-c73254f41c98
keywords:
- CM_PROB_DUPLICATE_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98cc72f297d125b5f55d64f6d02833a432cf7c32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342388"
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

    ここでお問い合わせください[Microsoft サポート](http://support.microsoft.com/)にこの問題に問い合わせます。
