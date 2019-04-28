---
title: OPM と ChangeDisplaySettingsEx
description: OPM と ChangeDisplaySettingsEx
ms.assetid: 973a8481-4d9a-4272-9138-666c6e41ad89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6fc517b9264785635963dcf5ec839874fce350
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379858"
---
# <a name="opm-and-changedisplaysettingsex"></a>OPM と ChangeDisplaySettingsEx


アナログ コンテンツ保護 (ACP) を Microsoft win32 レベルのアプリケーションを変更できるため、 **ChangeDisplaySettingsEx**関数、ディスプレイのミニポート ドライバーを確認してください、ACP 保護の調整が入力を通じて**ChangeDisplaySettingsEx**はによって行われる調整に依存しない、 **IOPMVideoOutput**インターフェイス。 つまり、表示ミニポート ドライバーの物理的なコネクタで ACP 保護の種類が設定されている場合[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数、ディスプレイのミニポート ドライバー必要があります物理コネクタ経由で ACP 保護の種類を無効にすると許可されていない、 [ **IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)要求。 ユーザー モードへの呼び出しに注意してください。 **ChangeDisplaySettingsEx** IOCTL 開始\_ビデオ\_処理\_表示ミニポート ドライバーに VIDEOPARAMETERS 要求。

詳細については、 **ChangeDisplaySettingsEx**関数を Microsoft Windows SDK のマニュアルを参照してください。

 

 





