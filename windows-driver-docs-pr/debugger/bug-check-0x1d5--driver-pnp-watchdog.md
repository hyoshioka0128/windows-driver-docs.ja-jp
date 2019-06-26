---
title: バグ チェック 0x1D5 DRIVER_PNP_WATCHDOG
description: DRIVER_PNP_WATCHDOG のバグ チェックでは、0x000001D5 の値を持ちます。 システム ワイドなウォッチドッグの有効期限が切れています。 これは、そのドライバーを特定の時間内での PnP の操作を完了できませんでしたを示します。
keywords:
- バグ チェック 0x1D5 DRIVER_PNP_WATCHDOG
- DRIVER_PNP_WATCHDOG
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- DRIVER_PNP_WATCHDOG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d262f47862807396cbd33f22c69f373e55074dd9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361984"
---
# <a name="bug-check-0x1d5-driverpnpwatchdog"></a>バグ チェック 0x1D5:ドライバー\_PNP\_ウォッチドッグ

ドライバー\_PNP\_ウォッチドッグのバグ チェックが 0x000001D5 の値を持ちます。 これは、特定の時間内での PnP 操作を完了するドライバーが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。

 

## <a name="driverpnpwatchdog-parameters"></a>ドライバー\_PNP\_ウォッチドッグ パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| Devnode に関連付けられているサービスのいくつかの最初の文字。|
|2| Nt へのポインター。TRIAGE_PNP_WATCHDOG Win10 RS4 以降。 |
|3| スレッドの PnP、ウォッチドッグを担当します。|
|4| ウォッチドッグの武装経過時間 (ミリ秒)。 |


## <a name="cause"></a>原因
-----

これは、特定の時間内での PnP 操作を完了するドライバーが失敗したことを示します。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

