---
title: OPM と ChangeDisplaySettingsEx
description: OPM と ChangeDisplaySettingsEx
ms.assetid: 973a8481-4d9a-4272-9138-666c6e41ad89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 257b5407c5e7bfa10d5fed56669cb5be3ab70bc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840498"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM と ChangeDisplaySettingsEx


アプリケーションでは、Microsoft Win32 **Changedisplaysettingsex**関数を呼び出すことによってアナログコンテンツ保護 (ACP) レベルを変更できるため、ディスプレイミニポートドライバーは、を使用**して、acp 保護の種類に対する調整をChangeDisplaySettingsEx**は、 **IOPMVideoOutput**インターフェイスによって行われる調整に依存しません。 つまり、ディスプレイミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数を使用して、物理コネクタに対して acp 保護の種類が設定されている場合、ディスプレイミニポートドライバーでは、[**IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)の物理コネクタ\_VIDEOPARAMETERS 要求を処理します。 **Changedisplaysettingsex sex**のユーザーモード呼び出しでは、VIDEOPARAMETERS ビデオ\_ハンドルを処理して、ディスプレイミニポートドライバーへの要求を処理\_ことに注意してください。\_

**Changedisplaysettingsex**関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





