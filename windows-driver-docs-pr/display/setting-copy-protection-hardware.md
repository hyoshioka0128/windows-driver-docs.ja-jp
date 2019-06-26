---
title: コピー防止ハードウェアの設定
description: コピー防止ハードウェアの設定
ms.assetid: c9733d74-faa8-44af-8de7-9530ebcfe949
keywords:
- 保護設定の WDK ビデオ ミニポートをコピーします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d091be6c1e0db85d83196b8062c92d4951e27fb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365579"
---
# <a name="setting-copy-protection-hardware"></a>コピー防止ハードウェアの設定


## <span id="ddk_setting_copy_protection_hardware_gg"></span><span id="DDK_SETTING_COPY_PROTECTION_HARDWARE_GG"></span>


担当副社長が返されるミニポート ドライバー\_フラグ\_で保護されている[ **VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)の**dwFlags** VP メンバー\_コマンド\_GET VP への応答では、次を行う必要があります\_コマンド\_に応じて、SET コマンド、 **dwCPCommand** VIDEOPARAMETERS 構造体のメンバー。

-   場合**dwCPCommand**担当副社長は\_CP\_CMD\_アクティブ化、ミニポート ドライバーがコピー保護をオン生成して返す内の一意のコピー保護キーを**dwCPKey**.

-   場合**dwCPCommand**担当副社長は\_CP\_CMD\_でキーの非アクティブ化とコピー防止**dwCPKey**有効ですが、ミニポート ドライバーは、コピー防止をオフにする必要があります。

-   場合**dwCPCommand**担当副社長は\_CP\_CMD\_でキーを変更し、コピー防止**dwCPKey**有効ですが、ミニポート ドライバーに基づくコピー防止を変更する必要があります、内のデータは、トリガーのデータに基づく**bCP\_APSTriggerBits**します。

コピー防止のハードウェアがないデバイスのミニポート ドライバーを返すだけいいえ\_でエラー、**状態**のフィールド、 [ **VRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)の**StatusBlock**します。

 

 





