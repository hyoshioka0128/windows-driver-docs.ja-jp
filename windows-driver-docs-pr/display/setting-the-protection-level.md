---
title: 保護レベルの設定
description: 保護レベルの設定
ms.assetid: e0fecc58-59d9-470a-83e6-9b08e2f59169
keywords:
- WDK COPP、保護レベルの保護をコピーします。
- ビデオのコピー防止 WDK COPP、保護レベル
- COPP WDK DirectX va なので、保護レベル
- ビデオの WDK COPP、保護レベルの保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6320a24a62220d918f71164507139fee7578e6ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365541"
---
# <a name="setting-the-protection-level"></a>保護レベルの設定


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

COPP コマンドは、DirectX VA COPP デバイスに関連付けられた物理コネクタの保護の種類の保護レベルを設定できます。 レベルを設定する、保護、ビデオのミニポート ドライバーの[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数へのポインターを受け取る、 [ **DXVA\_COPPCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand)構造体、 **guidCommandID**メンバーは、DXVA に設定\_COPPSetProtectionLevel GUID と**CommandData**メンバーのセットをへのポインターに[ **DXVA\_COPPSetProtectionLevelCmdData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppsetprotectionlevelcmddata)セットと、保護を設定するレベルに保護の種類を指定する構造体。 保護レベルが保護の種類を使用できない場合、保護レベルは COPP に設定 COPP コマンド\_NoProtectionLevelAvailable (-1)。 COPP コマンドがの一部の拡張情報を指定しても、 **ExtendedInfoChangeMask**と**ExtendedInfoData**の DXVA メンバー\_ビデオの COPPSetProtectionLevelCmdDataミニポート ドライバーの保護の種類を設定します。

指定した保護の種類は、次の保護レベルを設定できます。

-   COPP の\_ProtectionType\_ACP では、設定から、次の値の 1 つ、 **COPP\_ACP\_保護\_レベル**列挙型。
    -   COPP\_ACP\_Level0 または COPP\_ACP\_LevelMin (0)
    -   COPP\_ACP\_Level1 (1)
    -   COPP\_ACP\_Level2 (2)
    -   COPP\_ACP\_Level3 または COPP\_ACP\_LevelMax (3)

<!-- -->

-   COPP の\_ProtectionType\_CGMSA、設定から、次の値の 1 つ、 **COPP\_CGMSA\_保護\_レベル**列挙型。
    -   COPP\_CGMSA\_無効または COPP\_CGMSA\_LevelMin (0)
    -   COPP\_CGMSA\_CopyFreely (1)
    -   COPP\_CGMSA\_CopyNoMore (2)
    -   COPP\_CGMSA\_CopyOneGeneration (3)
    -   COPP\_CGMSA\_CopyNever (4)
    -   COPP\_CGMSA\_RedistributionControlRequired (0x08)
    -   (COPP\_CGMSA\_RedistributionControlRequired + COPP\_CGMSA\_CopyNever) または COPP\_CGMSA\_LevelMax

<!-- -->

-   COPP の\_ProtectionType\_HDCP 設定から、次の値の 1 つ、 **COPP\_HDCP\_保護\_レベル**列挙型。
    -   COPP\_HDCP\_Level0 または COPP\_HDCP\_LevelMin (0)
    -   COPP\_HDCP\_Level1 または COPP\_HDCP\_LevelMax (1)

 

 





