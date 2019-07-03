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
ms.openlocfilehash: a184b3b62bf46131b7254f7f13f698c422534652
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519649"
---
# <a name="bug-check-0x1d5-driverpnpwatchdog"></a>バグ チェック 0x1D5:ドライバー\_PNP\_ウォッチドッグ

ドライバー\_PNP\_ウォッチドッグのバグ チェックが 0x000001D5 の値を持ちます。 これは、特定の時間内での PnP 操作を完了するドライバーが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

 

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

