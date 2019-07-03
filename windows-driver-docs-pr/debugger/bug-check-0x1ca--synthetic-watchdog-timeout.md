---
title: バグ チェック 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
description: SYNTHETIC_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001CA の値を持ちます。 システム ワイドなウォッチドッグの有効期限が切れています。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。
keywords:
- バグ チェック 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
- SYNTHETIC_WATCHDOG_TIMEOUT
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- SYNTHETIC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b3b3c470d3ecd98f0c1b0420d22581f263ceeb8
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519703"
---
# <a name="bug-check-0x1ca-syntheticwatchdogtimeout"></a>バグ チェック 0x1CA:代理\_ウォッチドッグ\_タイムアウト

統合、\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001CA の値を持ちます。 システム ワイドなウォッチドッグの有効期限が切れています。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

 

## <a name="syntheticwatchdogtimeout-parameters"></a>代理\_ウォッチドッグ\_タイムアウト パラメーター

|パラメーター|説明|
|-------- |---------- |
|1|ウォッチドッグが最後にリセット、割り込み時間の時間。|
|2| 現在の割り込み時間。 |
|3| QPC の現在のタイムスタンプ。 |
|4| クロックのプロセッサのインデックス。 |

## <a name="cause"></a>原因
-----

システム ワイドなウォッチドッグの有効期限が切れています。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

