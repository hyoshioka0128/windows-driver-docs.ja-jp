---
title: CM_PROB_WAITING_ON_DEPENDENCY
description: CM_PROB_WAITING_ON_DEPENDENCY
ms.assetid: 2f45c507-1926-47f4-aca8-f8b834c58601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c500f222e940296e6f78fb0f7fd84877421caf78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375341"
---
# <a name="cmprobwaitingondependency"></a>CM_PROB_WAITING_ON_DEPENDENCY

この関数は、システムの使用に予約されています。

開始されていない別のデバイスで依存関係があるために、デバイスは開始されませんでした。

## <a name="error-code"></a>エラー コード

51

### <a name="display-message"></a>メッセージを表示します。

"このデバイスは、別のデバイスまたはデバイスのセットで現在待機中です。 (コード 51)"です。

### <a name="recommended-resolution"></a>推奨される解決方法

現在、この問題の解決方法はありません。

その他を調べたり、問題の診断に役立つ内のデバイスに失敗しました、[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)をこのデバイスに依存します。 別の関連するデバイスが起動されなかった理由を指定できます、この問題を解決できる可能性があります。
