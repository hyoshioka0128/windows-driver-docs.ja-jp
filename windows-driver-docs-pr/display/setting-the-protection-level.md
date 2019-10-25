---
title: 保護レベルの設定
description: 保護レベルの設定
ms.assetid: e0fecc58-59d9-470a-83e6-9b08e2f59169
keywords:
- コピー防止 WDK COPP、保護レベル
- ビデオコピー防止 WDK COPP、保護レベル
- COPP WDK DirectX VA、保護レベル
- 保護されたビデオ WDK COPP、保護レベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8ac297866e20b52b2e3b63f3ff610954e31ce2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825810"
---
# <a name="setting-the-protection-level"></a>保護レベルの設定


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

COPP コマンドは、DirectX VA COPP デバイスに関連付けられている物理コネクタで、保護の種類の保護レベルを設定できます。 保護レベルを設定するために、ビデオミニポートドライバーの[*coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数は、 **GUIDCOMMANDID**メンバーが DXVA\_COPPSETPROTECTIONLEVEL GUID に設定された[**DXVA\_coppcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)構造体へのポインターを受け取ります。**Commanddata**メンバーが、設定する保護の種類と保護を設定するレベルを指定する[**DXVA\_COPPSetProtectionLevelCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetprotectionlevelcmddata)構造体へのポインターに設定されます。 保護の種類で保護レベルを使用できない場合は、COPP コマンドによって保護レベルが COPP\_NoProtectionLevelAvailable (-1) に設定されます。 また、COPP コマンドでは、DXVA\_COPPSetProtectionLevelCmdData の**Extendedinfochangemask**および**extendedinfodata**メンバーの拡張情報を指定して、ビデオミニポートドライバーで保護の種類を設定することもできます。

次の保護レベルは、指定された保護の種類に対して設定できます。

-   \_ProtectionType\_ACP の場合は、次のいずれかの値を**copp\_acp\_Protection\_Level**列挙型から設定します。
    -   \_ACP\_Level0 または COPP\_ACP\_LevelMin (0)
    -   \_ACP\_Level1 (1)
    -   \_ACP\_Level2 (2)
    -   \_ACP\_Level3 または COPP\_ACP\_LevelMax (3)

<!-- -->

-   COPP\_ProtectionType\_CGMSA の場合は、次のいずれかの値を**copp\_CGMSA\_Protection\_Level**列挙型から設定します。
    -   COPP\_CGMSA\_Disabled または COPP\_CGMSA\_LevelMin (0)
    -   COPP\_CGMSA\_CopyFreely (1)
    -   COPP\_CGMSA\_CopyNoMore (2)
    -   COPP\_CGMSA\_CopyOneGeneration (3)
    -   COPP\_CGMSA\_CopyNever (4)
    -   COPP\_CGMSA\_RedistributionControlRequired (0x08)
    -   (COPP\_CGMSA\_Reて Controlrequired + COPP\_CGMSA\_CopyNever) または COPP\_CGMSA\_LevelMax

<!-- -->

-   COPP\_ProtectionType\_HDCP では、次のいずれかの値を**copp\_hdcp\_Protection\_Level**列挙型から設定します。
    -   COPP\_HDCP\_Level0 または COPP\_HDCP\_LevelMin (0)
    -   COPP\_HDCP\_Level1 または COPP\_HDCP\_LevelMax (1)

 

 





