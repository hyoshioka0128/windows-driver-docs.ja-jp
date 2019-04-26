---
title: COPP と ChangeDisplaySettingsEx
description: COPP と ChangeDisplaySettingsEx
ms.assetid: 5c729bfd-0758-4de5-9e81-a3279f8aab56
keywords:
- 保護 WDK COPP、ChangeDisplaySettingsEx をコピーします。
- ビデオのコピー防止 WDK COPP、ChangeDisplaySettingsEx
- COPP WDK DirectX va なので、ChangeDisplaySettingsEx
- ビデオの WDK COPP ChangeDisplaySettingsEx の保護
- ChangeDisplaySettingsEx
- アナログ コンテンツ保護 WDK COPP
- 保護の種類の ACP WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bcde3a67ea1038eb92ffa3100088852ac8a7bff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346918"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP と ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

アナログ コンテンツ保護 (ACP) を Microsoft win32 レベルのアプリケーションを変更できるため、 **ChangeDisplaySettingsEx**関数の場合、ビデオのミニポート ドライバーを確認してください、ACP 保護の調整がを通じて型を**ChangeDisplaySettingsEx**はによって行われる調整に依存しない、 **IAMCertifiedOutputProtection**インターフェイス。 つまり、ビデオのミニポート ドライバーの物理的なコネクタで ACP 保護の種類が設定されている場合[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)関数の場合、ビデオのミニポート ドライバーを許可すべき、ACP を無効にします。保護の種類の物理コネクタ経由で、 [ **IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)要求。 ユーザー モードへの呼び出しに注意してください。 **ChangeDisplaySettingsEx** IOCTL 開始\_ビデオ\_処理\_ビデオのミニポート ドライバーに VIDEOPARAMETERS 要求。

詳細については、 **ChangeDisplaySettingsEx**関数を Windows SDK のマニュアルを参照してください。

 

 





