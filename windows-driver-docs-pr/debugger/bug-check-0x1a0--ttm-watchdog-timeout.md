---
title: バグ チェック 0x1A0 TTM_WATCHDOG_TIMEOUT
description: TTM_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001A0 の値を持ちます。 これは、ターミナル トポロジ manager に構成されているタイムアウトの特定のデバイス操作完了しなかったことが検出されたことを示します。
keywords:
- バグ チェック 0x1A0 TTM_WATCHDOG_TIMEOUT
- TTM_WATCHDOG_TIMEOUT
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- TTM_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cefaa99841c08b8093f66b735750d291c4d5a91b
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761831"
---
# <a name="bug-check-0x1a0-ttmwatchdogtimeout"></a>バグ チェック 0x1A0 の。TTM\_ウォッチドッグ\_タイムアウト

TTM\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x000001A0 の値を持ちます。 これは、ターミナル トポロジ manager に構成されているタイムアウトの特定のデバイス操作完了しなかったことが検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="ttmwatchdogtimeout-parameters"></a>TTM\_ウォッチドッグ\_タイムアウト パラメーター

|パラメーター|説明|
|--- |--- |
|1| エラーの種類の値以下に示します。|
|2| デバイスへのポインター。 |
|3| ワーカー スレッドへのポインター。|
|4| 引き出し線のルーチンへのポインター。 |

**エラーの種類**

0x1:ターミナルにデバイスの割り当てが進行をしていません。

0x2:デバイスの閉じるコールバックが進行をしていません。

0x3:デバイスの入力モードを設定のコールバックが進行をしていません。

0x4:デバイスの表示状態の設定のコールバックが進行をしていません。

0x5。デバイスの組み込みのパネルの状態を設定しても、進行状況が行われていません。

0x6:デバイスのプライマリ ディスプレイの表示状態の更新が進行をしていません。

## <a name="cause"></a>原因
-----

ターミナル トポロジ マネージャーでは、構成されたタイムアウトの特定のデバイス操作完了しなかったことが検出されました。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

