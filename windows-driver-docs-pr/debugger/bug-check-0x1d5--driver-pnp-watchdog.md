---
title: バグチェック 0x1D5 DRIVER_PNP_WATCHDOG
description: DRIVER_PNP_WATCHDOG のバグチェックには、0x000001D5 という値が指定されています。 システム全体のウォッチドッグの有効期限が切れています。 これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。
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
ms.openlocfilehash: c2a7e051f6bfadd0c607cc500784468008d566f7
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916229"
---
# <a name="bug-check-0x1d5-driver_pnp_watchdog"></a>バグチェック 0x1D5: ドライバー\_PNP\_ウォッチドッグ

ドライバー\_PNP\_ウォッチドッグのバグチェックには、0x000001D5 という値が指定されています。 これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

 

## <a name="driver_pnp_watchdog-parameters"></a>ドライバー\_PNP\_ウォッチドッグパラメーター

|パラメーター|説明|
|-------- |---------- |
|1| Devnode に関連付けられているサービスの最初の数文字。|
|2| Nt へのポインターTRIAGE_PNP_WATCHDOG Win10 RS4 以降。 |
|3| PnP ウォッチドッグを担当するスレッド。|
|ホーム フォルダーが置かれているコンピューターにアクセスできない| ウォッチドッグが行われてからの経過時間 (ミリ秒)。 |


## <a name="cause"></a>原因
-----

これは、ドライバーが特定の時間内に PnP 操作を完了できなかったことを示します。 ! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。


## <a name="see-also"></a>参照
----------

[バグチェックコードリファレンス](bug-check-code-reference2.md)

