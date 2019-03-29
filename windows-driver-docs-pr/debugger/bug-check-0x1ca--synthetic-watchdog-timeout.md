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
ms.openlocfilehash: 557839ebdf7bce8354dae79c9e8566ab95734b19
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743571"
---
# <a name="bug-check-0x1ca-syntheticwatchdogtimeout"></a>バグ チェック 0x1CA の。代理\_ウォッチドッグ\_タイムアウト

統合、\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001CA の値を持ちます。 システム ワイドなウォッチドッグの有効期限が切れています。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

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

