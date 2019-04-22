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
ms.openlocfilehash: aa6ed66a0f3def21454639270783f7b0c8940c82
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238521"
---
# <a name="bug-check-0x1db-ipiwatchdogtimeout"></a>バグ チェック 0x1DB:IPI\_ウォッチドッグ\_タイムアウト

IPI\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001DB の値を持ちます。 これは、プロセッサが許可されている時間より IPI ループになってされていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

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

