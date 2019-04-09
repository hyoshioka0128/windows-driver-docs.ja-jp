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
ms.openlocfilehash: 52cc555d8c8384994a70b66377dca57cbd2dcd0e
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238613"
---
# <a name="bug-check-bug-check-0x1cf-hardwarewatchdogtimeout"></a>チェックのバグ チェック 0x1CF をバグします。ハードウェア\_ウォッチドッグ\_タイムアウト 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


HARDWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001CF の値を持ちます。 これは、システムがハングし処理していなかったのタイマー刻みであることを示します。


## <a name="hardwarewatchdogtimeout-parameters"></a>ハードウェア\_ウォッチドッグ\_タイムアウト パラメーター
 
パラメーター | 説明 
|---------|--------------|
1 | ウォッチドッグが最後にリセット、割り込み時間の時間。
2 | 現在の割り込み時間。
3 | QPC の現在のタイムスタンプ。
4 | クロックのプロセッサのインデックス。


 

 




