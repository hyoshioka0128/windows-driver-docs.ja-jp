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
ms.openlocfilehash: b570272f29bf2878e4dde15d28da6e64f2c1ae27
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743538"
---
# <a name="bug-check-0x1db-ipiwatchdogtimeout"></a>バグ チェック 0x1DB の。IPI\_ウォッチドッグ\_タイムアウト

IPI\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001DB の値を持ちます。 これは、プロセッサが許可されている時間より IPI ループになってされていることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

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

