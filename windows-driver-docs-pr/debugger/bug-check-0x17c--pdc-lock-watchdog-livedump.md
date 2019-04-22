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
ms.openlocfilehash: 7780040a8ea85e59839578604848c70a63be6eed
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238773"
---
# <a name="bug-check-17c-pdclockwatchdoglivedump"></a>バグのチェック 17 C:PDC\_ロック\_ウォッチドッグ\_LIVEDUMP

PDC\_ロック\_ウォッチドッグ\_LIVEDUMP バグ チェックが 0x0000017C の値を持ちます。 これは、長時間 PDC ロックがスレッドの保持されていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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


 




