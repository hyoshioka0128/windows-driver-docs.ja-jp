---
title: バグ チェック 0x1DB IPI_WATCHDOG_TIMEOUT
description: IPI_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001DB の値を持ちます。 プロセッサがされていることを示します、許可されている時間より IPI ループになっています。
keywords:
- バグ チェック 0x1DB IPI_WATCHDOG_TIMEOUT
- IPI_WATCHDOG_TIMEOUT
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- IPI_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d234677ac0dc58d994e714c2439962bf5f8a8c3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367562"
---
# <a name="bug-check-0x1db-ipiwatchdogtimeout"></a>バグ チェック 0x1DB:IPI\_ウォッチドッグ\_タイムアウト

IPI\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001DB の値を持ちます。 これは、プロセッサが許可されている時間より IPI ループになってされていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。

 

## <a name="ipiwatchdogtimeout-parameters"></a>IPI\_ウォッチドッグ\_タイムアウト パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| QPC の頻度を示します。  |
|2| 現在の QPC を示します。 |
|3| QPC の基準を示します。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----

許可された時間より多くのプロセッサをスタック IPI ループにするとします。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

