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
ms.openlocfilehash: 3a4a8a3e23094476f0bf3f09e34a6b8c187ef40b
ms.sourcegitcommit: f931a1bad4132c07be5966b428c77745c96bcba4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2020
ms.locfileid: "77340087"
---
# <a name="bug-check-bug-check-0x1a2-win32k_callout_watchdog_bugcheck"></a>バグチェックのバグチェック 0x1A2: WIN32K\_コールアウト\_ウォッチドッグ\_バグチェック

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

WIN32K\_コールアウト\_ウォッチドッグ\_バグチェックライブダンプの値は0x000001A2 です。 これは、Win32k へのコールアウトがすぐに戻らなかったことを示します。

## <a name="win32k_callout_watchdog_bugcheck-parameters"></a>WIN32K\_コールアウト\_ウォッチドッグ\_のバグチェックパラメーター

次のパラメーターがブルースクリーンに表示されます。

| パラメーター |                        説明                    |
|-----------|-------------------------------------------------------|
|     1     | スレッドブロックプロンプトは、Win32k コールアウトから戻ります。  |
|     2     | 予約済み。                                             |
|     3     | 予約済み。                                             |
|     4     | 予約済み。                                             |
