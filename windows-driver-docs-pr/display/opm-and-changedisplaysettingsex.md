---
title: OPM と ChangeDisplaySettingsEx
description: OPM と ChangeDisplaySettingsEx
ms.assetid: 973a8481-4d9a-4272-9138-666c6e41ad89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b944ab2c5b981d76b432cb76df866dee4475023
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372766"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM と ChangeDisplaySettingsEx


アナログ コンテンツ保護 (ACP) を Microsoft win32 レベルのアプリケーションを変更できるため、 **ChangeDisplaySettingsEx**関数、ディスプレイのミニポート ドライバーを確認してください、ACP 保護の調整が入力を通じて**ChangeDisplaySettingsEx**はによって行われる調整に依存しない、 **IOPMVideoOutput**インターフェイス。 つまり、表示ミニポート ドライバーの物理的なコネクタで ACP 保護の種類が設定されている場合[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数、ディスプレイのミニポート ドライバー必要があります物理コネクタ経由で ACP 保護の種類を無効にすると許可されていない、 [ **IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)要求。 ユーザー モードへの呼び出しに注意してください。 **ChangeDisplaySettingsEx** IOCTL 開始\_ビデオ\_処理\_表示ミニポート ドライバーに VIDEOPARAMETERS 要求。

詳細については、 **ChangeDisplaySettingsEx**関数を Microsoft Windows SDK のマニュアルを参照してください。

 

 





