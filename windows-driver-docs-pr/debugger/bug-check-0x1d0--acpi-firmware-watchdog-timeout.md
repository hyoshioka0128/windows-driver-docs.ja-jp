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
ms.openlocfilehash: 9ed010872ac2d2b3fe9dc29e6a22d0779ba4d5e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367582"
---
# <a name="bug-check-bug-check-0x1d0-acpifirmwarewatchdogtimeout"></a>チェックのバグ チェック 0x1D0 をバグします。ACPI\_ファームウェア\_ウォッチドッグ\_タイムアウト 


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


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





