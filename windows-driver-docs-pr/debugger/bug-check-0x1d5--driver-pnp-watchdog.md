---
title: バグチェック 0x1D5 DRIVER_PNP_WATCHDOG
description: DRIVER_PNP_WATCHDOG のバグチェックには、0x000001D5 という値があります。 システム全体のウォッチドッグの有効期限が切れています。 これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。
keywords:
- バグチェック 0x1D5 DRIVER_PNP_WATCHDOG
- DRIVER_PNP_WATCHDOG
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- DRIVER_PNP_WATCHDOG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 308a2385b635cee0119e28c95aef81ed2b736682
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534831"
---
# <a name="bug-check-0x1d5-driver_pnp_watchdog"></a>バグチェック 0x1D5: ドライバーの \_ PNP \_ ウォッチドッグ

ドライバーの \_ PNP \_ ウォッチドッグのバグチェックには、0x000001D5 という値が指定されています。 これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

 

## <a name="driver_pnp_watchdog-parameters"></a>ドライバーの \_ PNP \_ ウォッチドッグパラメーター

|パラメーター|説明|
|-------- |---------- |
|1| Devnode に関連付けられているサービスの最初の数文字。|
|2| Nt へのポインターWin10 RS4 以降では TRIAGE_PNP_WATCHDOG。 |
|3| PnP ウォッチドッグを担当するスレッド。|
|4| ウォッチドッグが行われてからの経過時間 (ミリ秒)。 |


## <a name="cause"></a>原因
-----

これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。 ! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。


## <a name="see-also"></a>参照
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

