---
title: バグ チェック 0x1D0 ACPI_FIRMWARE_WATCHDOG_TIMEOUT
description: ACPI_FIRMWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001D0 の値を持ちます。
keywords:
- バグ チェック 0x1D0 ACPI_FIRMWARE_WATCHDOG_TIMEOUT
- ACPI_FIRMWARE_WATCHDOG_TIMEOUT
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- ACPI_FIRMWARE_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72688bd601555ddad3e4c501ccb6a4f933609bc9
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519674"
---
# <a name="bug-check-bug-check-0x1d0-acpifirmwarewatchdogtimeout"></a>チェックのバグ チェック 0x1D0 をバグします。ACPI\_ファームウェア\_ウォッチドッグ\_タイムアウト 


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


ACPI_FIRMWARE_WATCHDOG_TIMEOUT のバグ チェックでは、0x000001D0 の値を持ちます。 

ACPI ドライバーは、予想される割り当てられた時間内の操作を完了できませんでした。

## <a name="acpifirmwarewatchdogtimeout-parameters"></a>ACPI\_ファームウェア\_ウォッチドッグ\_タイムアウト パラメーター

次のパラメーターは、ブルー スクリーンに表示されます。

パラメーター | 説明 
|---------|--------------|
1 | AMLI コンテキストへのポインター
2 | Aml コンテキストの名前を Unicode へのポインター
3 | ACPI デバイス拡張機能へのポインター。
4 | ACPI トリアージ ブロックへのポインター。





