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
ms.openlocfilehash: 715bc8cde74b247e4fec4f6b44c27eb395434af3
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239115"
---
# <a name="bug-check-bug-check-0x1d0-acpifirmwarewatchdogtimeout"></a>チェックのバグ チェック 0x1D0 をバグします。ACPI\_ファームウェア\_ウォッチドッグ\_タイムアウト 


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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





