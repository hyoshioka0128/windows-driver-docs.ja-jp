---
title: バグ チェック 0x1CF HARDWARE_WATCHDOG_TIMEOUT
description: HARDWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001CF の値を持ちます。
keywords:
- バグ チェック 0x1CF HARDWARE_WATCHDOG_TIMEOUT
- HARDWARE_WATCHDOG_TIMEOUT
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- HARDWARE_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4fd2513c1ddbf0522d80dfdb93a585f3e820c289
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519678"
---
# <a name="bug-check-bug-check-0x1cf-hardwarewatchdogtimeout"></a>チェックのバグ チェック 0x1CF をバグします。ハードウェア\_ウォッチドッグ\_タイムアウト 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


HARDWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001CF の値を持ちます。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。


## <a name="hardwarewatchdogtimeout-parameters"></a>ハードウェア\_ウォッチドッグ\_タイムアウト パラメーター
 
パラメーター | 説明 
|---------|--------------|
1 | ウォッチドッグが最後にリセット、割り込み時間の時間。
2 | 現在の割り込み時間。
3 | QPC の現在のタイムスタンプ。
4 | クロックのプロセッサのインデックス。


 

 




