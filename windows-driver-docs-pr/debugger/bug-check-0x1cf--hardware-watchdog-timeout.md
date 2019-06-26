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
ms.openlocfilehash: e53d5ff809cd86c40726c4f1488416a5787f37af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367588"
---
# <a name="bug-check-bug-check-0x1cf-hardwarewatchdogtimeout"></a>チェックのバグ チェック 0x1CF をバグします。ハードウェア\_ウォッチドッグ\_タイムアウト 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


HARDWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001CF の値を持ちます。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。


## <a name="hardwarewatchdogtimeout-parameters"></a>ハードウェア\_ウォッチドッグ\_タイムアウト パラメーター
 
パラメーター | 説明 
|---------|--------------|
1 | ウォッチドッグが最後にリセット、割り込み時間の時間。
2 | 現在の割り込み時間。
3 | QPC の現在のタイムスタンプ。
4 | クロックのプロセッサのインデックス。


 

 




