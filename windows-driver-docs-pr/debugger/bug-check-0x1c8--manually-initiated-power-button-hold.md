---
title: バグ チェック 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
description: MANUALLY_INITIATED_POWER_BUTTON_HOLD のバグ チェックでは、0x000001CE の値を持ちます。 ユーザーは、[電源] ボタンを保持しているときのバグチェックを開始する、システムが構成されました。
keywords:
- バグ チェック 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
ms.date: 09/24/2018
topic_type:
- apiref
api_name:
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93a96aed1f545cfcf98d4e224ec18a0c5abba6bd
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519710"
---
# <a name="bug-check-0x1c8-manuallyinitiatedpowerbuttonhold"></a>バグ チェック 0x1C8:手動で\_INITIATED\_POWER\_ボタン\_保持

手動で\_INITIATED\_POWER\_ボタン\_保留が 0x000001C8 の値を持ちます。

ユーザーが一定時間の電源ボタンを保持しているときのバグチェックを開始する、システムが構成されました。  これは、システムが時間の電源ボタンの保留中のハード リセットしようとしているときにダンプをキャプチャするために使用する診断バグチェックです。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


画面ではなく、標準的な"青"表示されているこのバグ チェックが発生したときに、黒の背景に、次のテキストが % 完了のインジケーターと共に表示されることに注意してください。

"[電源] ボタンをリリースしてください。 だけをシャット ダウンする秒。" 


## <a name="manuallyinitiatedpowerbuttonhold-parameters"></a>手動で\_INITIATED\_POWER\_ボタン\_保留パラメーター

次のパラメーターは、ブルー スクリーンに表示されます。

パラメーター | 説明 
|---------|--------------|
1 | 時間 (ミリ秒) のダウン、電源ボタンが開催されました。
2 | Nt へのポインター。 _POP_POWER_BUTTON_TRIAGE_BLOCK します。
3 | 予約済み。
4 | 予約済み。


 

 




