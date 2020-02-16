---
title: バグチェック 1A1 WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
description: WIN32K_CALLOUT_WATCHDOG_LIVEDUMP の値は0x000001A1 です。
keywords:
- バグチェック 0x1A1 WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
- WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
ms.date: 02/12/2020
topic_type:
- apiref
api_name:
- WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bfde3809e99a97da8951f62277d83704bc1d44d1
ms.sourcegitcommit: f931a1bad4132c07be5966b428c77745c96bcba4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2020
ms.locfileid: "77340085"
---
# <a name="bug-check-bug-check-0x1a1-win32k_callout_watchdog_livedump"></a>バグチェックのバグチェック 0x1A1: WIN32K\_吹き出し\_ウォッチドッグ\_LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

WIN32K\_コールアウト\_ウォッチドッグ\_LIVEDUMP ライブダンプの値は0x000001A1 です。 Win32k へのコールアウトはすぐには返されませんでした。

## <a name="win32k_callout_watchdog_livedump-parameters"></a>WIN32K\_コールアウト\_ウォッチドッグ\_LIVEDUMP Parameters

次のパラメーターがブルースクリーンに表示されます。

| パラメーター |                        説明                    |
|-----------|-------------------------------------------------------|
|     1     | スレッドブロックプロンプトは、Win32k コールアウトから戻ります。  |
|     2     | 予約済み。                                             |
|     3     | 予約済み。                                             |
|     4     | 予約済み。                                             |

## <a name="cause"></a>原因

Win32k へのコールアウトはすぐには返されませんでした。

(このコードは実際のバグチェックには使用できません。ライブダンプを識別するために使用されます)。
