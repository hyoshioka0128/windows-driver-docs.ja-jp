---
title: COPP と ChangeDisplaySettingsEx
description: COPP と ChangeDisplaySettingsEx
ms.assetid: 5c729bfd-0758-4de5-9e81-a3279f8aab56
keywords:
- コピー防止 WDK COPP、ChangeDisplaySettingsEx
- ビデオコピー防止 WDK COPP、ChangeDisplaySettingsEx
- COPP WDK DirectX VA、ChangeDisplaySettingsEx
- 保護されたビデオ WDK COPP、ChangeDisplaySettingsEx
- ChangeDisplaySettingsEx
- アナログコンテンツ保護 WDK COPP
- ACP 保護タイプ WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d38267a5945ba880cadd83a85bbf571b7ab722b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839040"
---
# <a name="copp-and-changedisplaysettingsex"></a>COPP と ChangeDisplaySettingsEx


## <span id="ddk_copp_and_changedisplaysettingsex_gg"></span><span id="DDK_COPP_AND_CHANGEDISPLAYSETTINGSEX_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

アプリケーションでは、Microsoft Win32 **Changedisplaysettingsex**関数を呼び出すことによってアナログコンテンツ保護 (ACP) レベルを変更できるため、ビデオミニポートドライバーは、を使用**して、acp 保護の種類をChangeDisplaySettingsEx**は、 **IAMCertifiedOutputProtection**インターフェイスによって行われる調整に依存しません。 つまり、ビデオミニポートドライバーの[*Coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数を使用して、物理コネクタで acp 保護の種類が設定されている場合、ビデオミニポートドライバーでは、物理コネクタでの acp 保護の種類の無効化を[**IOCTL\_VIDEO\_\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)要求を処理します。 **Changedisplaysettingsex**のユーザーモード呼び出しでは、ビデオミニポートドライバーへの VIDEOPARAMETERS 要求を処理\_、ビデオ\_ハンドル\_ます。

**Changedisplaysettingsex**関数の詳細については、Windows SDK のドキュメントを参照してください。

 

 





