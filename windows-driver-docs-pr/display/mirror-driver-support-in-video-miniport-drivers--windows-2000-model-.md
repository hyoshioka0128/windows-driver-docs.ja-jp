---
title: ビデオのミニポート ドライバー (XDDM) でミラー ドライバーのサポート
description: ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)
ms.assetid: ca91e0a6-d619-432a-829e-49012951f27c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、ミラー ドライバー
- ミラー ドライバー WDK Windows 2000 の表示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 381680b4d007517a71a5bdfca2a4683c5c57e57a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382323"
---
# <a name="mirror-driver-support-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)

*ミラー ドライバー*ミニポート ドライバーには、このようなサポートを試行する特別なコードが持つことはできませんので、Windows 2000 以降、ビデオのミニポート ドライバーが提供されますをサポートします。 参照してください[ミラー ドライバー](mirror-drivers.md)ミラーリング システムでのディスプレイ ドライバーの詳細についてはします。

ミラー ドライバーのミニポート ドライバーの要件はわずかです。 これを実装する必要がありますのみ関数は[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)、ミニポート ドライバー、および次によってエクスポートされます。

[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)

[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)

ミラー化されたサーフェイスに関連付けられた物理ディスプレイ デバイスがないため、上記の一覧に表示される関数の 3 つすべてを常に成功を返すための空の実装を使用できます。

**注**  以降 Windows 8 では、ミラー ドライバーがインストールされないシステムにします。 詳細については、次を参照してください。[ミラー ドライバー](mirror-drivers.md)します。

 

 

 





