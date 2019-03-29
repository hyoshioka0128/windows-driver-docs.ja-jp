---
title: バグ チェック 0x1A6 BLUETOOTH_ERROR_RECOVERY_LIVEDUMP
description: BLUETOOTH_ERROR_RECOVERY_LIVEDUMP のバグ チェックでは、0x000001A6 の値を持ちます。 これは、Bluetooth 無線ドライバーが irremediable 状態オプションをリセットしようとするエラーからの回復を開始したことを示します。
keywords:
- バグ チェック 0x1A6 BLUETOOTH_ERROR_RECOVERY_LIVEDUMP
- BLUETOOTH_ERROR_RECOVERY_LIVEDUMP
ms.date: 01/28/2019
topic_type:
- apiref
api_name:
- BLUETOOTH_ERROR_RECOVERY_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 119dd2b26349b845e696fcfb848053032395022f
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743554"
---
# <a name="bug-check-0x1a6-bluetootherrorrecoverylivedump"></a>バグ チェック 0x1A6 の。BLUETOOTH\_エラー\_RECOVERY\_LIVEDUMP

BLUETOOTH\_エラー\_RECOVERY\_LIVEDUMP バグ チェックが 0x000001A6 の値を持ちます。 これは、Bluetooth 無線ドライバー (bthport.sys) がエラーから回復し、ラジオ、irremediable 内部の状態をリセットしようとする回復を開始したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="bluetootherrorrecoverylivedump-parameters"></a>BLUETOOTH\_エラー\_RECOVERY\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| PDO の Bluetooth 無線 (デバイス)。|
|2| 予約済み。|
|3| 予約済み。|
|4| 予約済み。|

## <a name="cause"></a>原因
-----

Bluetooth 無線ドライバー (bthport.sys) は、回復し、ラジオ、irremediable 内部の状態をリセットしようとするエラーからの回復を開始しました。

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

