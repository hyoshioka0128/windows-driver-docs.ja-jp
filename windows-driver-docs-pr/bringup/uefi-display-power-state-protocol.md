---
title: UEFI の電源状態のプロトコルを表示します。
description: UEFI の電源状態のプロトコルを表示します。
ms.assetid: ab16c548-1402-4819-9fbb-a1d6f55d934a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db59ebd78497c04b6db27b85cce692e85835139c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556648"
---
# <a name="uefi-display-power-state-protocol"></a>UEFI の電源状態のプロトコルを表示します。


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

ディスプレイの電源状態プロトコルは、次のタスクを実行するために、UEFI バッテリの充電ドライバーとの通信に Microsoft UEFI バッテリの充電中のアプリケーションによって使用されます。

-   画面の電源を切り、バックライトのバッテリを 10 秒間、ユーザーの入力なし交互バッテリ UI を表示した後のモードの充電中にします。

-   戻り、画面とバックライトをバッテリ電源ボタンが押されたときに、モードを充電中にします。

**重要な**  UEFI バッテリのドライバーを充電する必要があります、このプロトコルを実装していません、デバイスは、カスタム UEFI バッテリが充電、Microsoft が提供するアプリケーションではなくアプリケーションを使用している場合。 Windows ブート マネージャーでは、ドライバーは、このプロトコルを実装している場合は、アプリケーションを課金 Microsoft UEFI バッテリを読み込みます。

 

Microsoft 提供の UEFI バッテリが充電アプリケーションの詳細については、[ブート環境でバッテリが充電中](battery-charging-in-the-boot-environment.md)を参照してください。

## <a name="protocol-interface"></a>プロトコル インターフェイス


-   [EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)

-   [EFI\_DISPLAY\_POWER\_PROTOCOL.SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)

-   [EFI\_DISPLAY\_POWER\_PROTOCOL.GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)

-   [EFI\_表示\_POWER\_状態](efi-display-power-state.md)

## <a name="related-topics"></a>関連トピック
[UEFI バッテリが充電アプリケーションのアーキテクチャ](architecture-of-the-uefi-battery-charging-application.md)  



