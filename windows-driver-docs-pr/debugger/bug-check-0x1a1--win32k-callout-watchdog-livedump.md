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
ms.openlocfilehash: 69a3e7fbf651f7d951b21594ba476ec7a2f87a02
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852125"
---
# <a name="bug-check-0x1a1-win32k_callout_watchdog_livedump"></a>バグチェック 0x1A1: WIN32K \_ 吹き出し \_ ウォッチドッグ \_ LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

WIN32K \_ コールアウト \_ ウォッチドッグ \_ LIVEDUMP ライブダンプの値は0x000001a1 です。 Win32k へのコールアウトはすぐには返されませんでした。

## <a name="win32k_callout_watchdog_livedump-parameters"></a>WIN32K \_ 吹き出し \_ ウォッチドッグ \_ LIVEDUMP パラメーター

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
