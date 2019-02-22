---
Description: Selective suspend is disabled for upgrade versions of Microsoft Windows XP. It is enabled for clean installations of Windows XP, Windows Vista, and later versions of Windows.
title: 選択的に有効化を中断
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b913f4206fb1d0eeae890e39f06395bd83ee637
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557453"
---
# <a name="enabling-selective-suspend"></a>選択的に有効化を中断


セレクティブ サスペンドのアップグレードのバージョンの Microsoft Windows XP は無効です。 Windows XP、Windows Vista、および以降のバージョンの Windows のクリーン インストールする場合は有効です。

選択的に有効にする特定のルート ハブとその子デバイスのサポートを中断、チェック ボックスをオンにする、**電源管理** タブで、USB ルート ハブの**デバイス マネージャー**します。

または、有効にできますかの値を設定して無効にする選択的なが中断**HcDisableSelectiveSuspend**の USB ポート ドライバー ソフトウェア キーの下。 選択的に 1 つの無効化の値を中断します。 選択的な 0 の有効値を中断します。

たとえば、Hydra OHCI コント ローラーの Usbport.inf 無効にする選択的には、次の行が中断します。

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

クライアント ドライバーは選択的かどうかを判断しようとはしないでください中断がアイドル状態の要求を送信する前に有効になっています。 デバイスのアイドル時間がアイドル状態の要求を送信する必要があります。 アイドル状態の要求が失敗すると、クライアント ドライバーがアイドル タイマーをリセットする必要があります、再試行しています。

## <a name="related-topics"></a>関連トピック


[USB のセレクティブ サスペンドします。](usb-selective-suspend.md)

[USB 電源管理](usb-power-management.md)

 

 





