---
title: バグチェック 1A2 WIN32K_CALLOUT_WATCHDOG_BUGCHECK
description: WIN32K_CALLOUT_WATCHDOG_BUGCHECK ライブダンプの値は0x000001A2 です。
keywords:
- バグチェック 0x1A2 WIN32K_CALLOUT_WATCHDOG_BUGCHECK
- WIN32K_CALLOUT_WATCHDOG_BUGCHECK
ms.date: 02/12/2020
topic_type:
- apiref
api_name:
- WIN32K_CALLOUT_WATCHDOG_BUGCHECK
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3e7a1973b07b6171b96f8dc696c1f62d9a6248c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852123"
---
# <a name="bug-check-0x1a2-win32k_callout_watchdog_bugcheck"></a>バグチェック 0x1A2: WIN32K \_ 吹き出し \_ ウォッチドッグの \_ バグチェック

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

WIN32K \_ 吹き出し \_ ウォッチドッグの \_ バグチェックのライブダンプには、0x000001a2 という値が指定されています。 これは、Win32k へのコールアウトがすぐに戻らなかったことを示します。

## <a name="win32k_callout_watchdog_bugcheck-parameters"></a>WIN32K \_ 吹き出し \_ ウォッチドッグの \_ バグチェックパラメーター

次のパラメーターがブルースクリーンに表示されます。

| パラメーター |                        説明                    |
|-----------|-------------------------------------------------------|
|     1     | スレッドブロックプロンプトは、Win32k コールアウトから戻ります。  |
|     2     | 予約済み。                                             |
|     3     | 予約済み。                                             |
|     4     | 予約済み。                                             |
