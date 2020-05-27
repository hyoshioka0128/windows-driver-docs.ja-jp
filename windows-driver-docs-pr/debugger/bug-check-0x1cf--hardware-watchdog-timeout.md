---
title: バグチェック 0x1CF HARDWARE_WATCHDOG_TIMEOUT
description: HARDWARE_WATCHDOG_TIMEOUT バグチェックの値は0x000001CF です。
keywords:
- バグチェック 0x1CF HARDWARE_WATCHDOG_TIMEOUT
- HARDWARE_WATCHDOG_TIMEOUT
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- HARDWARE_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbb23fa28b453adbe964cf9d0c0ac777bb988916
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851985"
---
# <a name="bug-check-0x1cf-hardware_watchdog_timeout"></a>バグチェック 0x1CF: ハードウェア \_ ウォッチドッグ \_ タイムアウト 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


HARDWARE_WATCHDOG_TIMEOUT バグチェックの値は0x000001CF です。 これは、システムがハングし、タイマー刻みを処理していないことを示します。


## <a name="hardware_watchdog_timeout-parameters"></a>ハードウェア \_ ウォッチドッグの \_ タイムアウトパラメーター
 
パラメーター | 説明 
|---------|--------------|
1 | ウォッチドッグが最後にリセットされてからの経過時間 (割り込み時間)。
2 | 現在の割り込み時間。
3 | 現在の QPC タイムスタンプ。
4 | クロックプロセッサのインデックス。


 

 




