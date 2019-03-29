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
ms.openlocfilehash: afe9cab920ff14f4c37b61eb4a2f75b2f39d4853
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743576"
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

     0x1 : A device assignment to a terminal is not making progress.
     0x2 : Device's close callback is not making progress.
     0x3 : Device's set-input-mode callback is not making progress.
     0x4 : Device's set-display-state callback is not making progress.
     0x5 : Setting device's built-in panel state is not making progress.
     0x6 : Updating device's primary display visible state is not making progress.

## <a name="cause"></a>原因
-----

ターミナル トポロジ マネージャーでは、構成されたタイムアウトの特定のデバイス操作完了しなかったことが検出されました。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

