---
title: バグ チェック 17 C PDC_LOCK_WATCHDOG_LIVEDUMP
description: PDC_LOCK_WATCHDOG_LIVEDUMP のバグ チェックでは、0x0000017C の値を持ちます。 これは、長時間 PDC ロックがスレッドの保持されていることを示します。
keywords:
- バグ チェック 17 C PDC_LOCK_WATCHDOG_LIVEDUMP
- PDC_LOCK_WATCHDOG_LIVEDUMP
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- PDC_LOCK_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92a7275813f2a17f85bf55836803a911e53ddf87
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743557"
---
# <a name="bug-check-17c-pdclockwatchdoglivedump"></a>バグのチェック 17 C:PDC\_ロック\_ウォッチドッグ\_LIVEDUMP

PDC\_ロック\_ウォッチドッグ\_LIVEDUMP バグ チェックが 0x0000017C の値を持ちます。 これは、長時間 PDC ロックがスレッドの保持されていることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 ## <a name="pdclockwatchdoglivedump-parameters"></a>PDC\_ロック\_ウォッチドッグ\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| PDC を保持しているスレッドをロックします。|
|2| ロックのウォッチドッグ タイムアウト (ミリ秒単位)。 |
|3| 予約済み。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----
スレッドが長時間 PDC ロックを保持しているがされています。 調査する情報を提供する、livedump が作成されます。 

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
-----

デバッガーを使用して[! スレッド](-thread.md)パラメーター 1 で提供されているロックを保持しているスレッドを表示するコマンド。  タイムアウト期間を超えたロックが保持するかを決定するには、そのコードを分析します。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

[!thread](-thread.md)


 




