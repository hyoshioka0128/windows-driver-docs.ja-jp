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
ms.openlocfilehash: 598714b117833f765b2d74a9cd0ad30e5df223a6
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238991"
---
# <a name="bug-check-0x1d5-driverpnpwatchdog"></a>バグ チェック 0x1D5:ドライバー\_PNP\_ウォッチドッグ

ドライバー\_PNP\_ウォッチドッグのバグ チェックが 0x000001D5 の値を持ちます。 これは、特定の時間内での PnP 操作を完了するドライバーが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

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

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

