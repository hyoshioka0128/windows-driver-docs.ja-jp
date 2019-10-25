---
title: コピー防止ハードウェアの設定
description: コピー防止ハードウェアの設定
ms.assetid: c9733d74-faa8-44af-8de7-9530ebcfe949
keywords:
- コピー防止 WDK ビデオミニポート、設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e643811e5a227b40cbfa34435db34faa8603e3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829503"
---
# <a name="setting-copy-protection-hardware"></a>コピー防止ハードウェアの設定


## <span id="ddk_setting_copy_protection_hardware_gg"></span><span id="DDK_SETTING_COPY_PROTECTION_HARDWARE_GG"></span>


Vp\_\_フラグを返したミニポートドライバーは、 VP\_コマンドの[ **\_GET で**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)、VP\_command\_SET コマンドに応答して、次の操作を行う必要があります。VIDEOPARAMETERS 構造体の**Dwcpcommand**メンバーに応じて、次のようになります。

-   **Dwcpcommand**が VP\_CP\_CMD\_ACTIVATE の場合、ミニポートドライバーはコピー防止をオンにして、 **dwcpcommand**で一意のコピー保護キーを生成して返します。

-   **Dwcpcommand**が VP\_CP\_CMD\_DEACTIVATE で、 **dwcpcommand**のコピー保護キーが有効である場合、ミニポートドライバーはコピー防止をオフにする必要があります。

-   **Dwcpcommand**が VP\_CP\_CMD\_CHANGE で、 **dwcpcommand**のコピー保護キーが有効である場合、データに基づいて、ミニポートドライバーは、 **\_bCP のトリガーデータに基づいてコピー保護を変更する必要があります。** .

コピー防止ハードウェアがないデバイスのミニポートドライバーは、 [**VRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)の**Statusblock**の**Status**フィールドに\_エラーが返されないようにする必要があります。

 

 





