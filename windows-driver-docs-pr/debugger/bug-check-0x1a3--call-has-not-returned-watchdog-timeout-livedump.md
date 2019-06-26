---
title: バグ チェック 1A3 CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP
description: CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP ライブ ダンプには、0x000001A3 の値があります。
keywords:
- バグ チェック 0x1A3 CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP
- CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/25/2018
topic_type:
- apiref
api_name:
- CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 60f58db71ff6c65a41c9adccf1bad55c5e08a196
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362036"
---
# <a name="bug-check-bug-check-0x1a3-callhasnotreturnedwatchdogtimeoutlivedump"></a>チェックのバグ チェック 0x1A3 をバグします。呼び出す\_HAS\_いない\_から返された\_ウォッチドッグ\_タイムアウト\_LIVEDUMP 


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


呼び出しがタイムアウト期間内は返されません。

CALL_HAS_NOT_RETURNED_WATCHDOG_TIMEOUT_LIVEDUMP ライブ ダンプには、0x000001A3 の値があります。 


## <a name="callhasnotreturnedwatchdogtimeoutlivedump-parameters"></a>呼び出す\_HAS\_いない\_から返された\_ウォッチドッグ\_タイムアウト\_LIVEDUMP パラメーター

次のパラメーターは、ブルー スクリーンに表示されます。


| パラメーター |                        説明                        |
|-----------|-----------------------------------------------------------|
|     1     | 呼び出しはすぐに返されませんが、スレッドのプロセス。 |
|     2     |       スレッドの呼び出しはすぐに返されません。        |
|     3     |                 タイムアウト (ミリ秒単位)。                  |
|     4     |    dt nt!_PO_CALL_HAS_NOT_RETURNED_WATCHDOG <address>     |

