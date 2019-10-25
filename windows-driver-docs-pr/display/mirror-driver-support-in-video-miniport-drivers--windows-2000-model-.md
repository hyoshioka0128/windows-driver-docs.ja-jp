---
title: ビデオミニポートドライバー (XDDM) でのミラードライバーのサポート
description: ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)
ms.assetid: ca91e0a6-d619-432a-829e-49012951f27c
keywords:
- ビデオミニポートドライバー WDK Windows 2000、ミラードライバー
- ミラードライバー WDK Windows 2000 ディスプレイ
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 22cb9caf6984ab2f2a13aa97393b3fe7b13ca101
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840562"
---
# <a name="mirror-driver-support-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)

ビデオミニポートドライバーに対する*ミラードライバー*のサポートは、Windows 2000 以降で提供されているため、ミニポートドライバーは、このようなサポートを試行する特別なコードを持っていてはなりません。 ミラーリングシステムのディスプレイドライバーの詳細については、「[ミラードライバー](mirror-drivers.md) 」を参照してください。

ミラードライバーミニポートドライバーの要件は最小限です。 実装する必要がある関数は、ミニポートドライバーによってエクスポートされる[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)と、次のとおりです。

[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)

[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)

ミラー化された画面には物理ディスプレイデバイスが関連付けられていないため、上記の一覧に示した3つの関数はすべて、常に成功を返す空の実装にすることができます。

**注**  Windows 8 以降では、ミラードライバーはシステムにインストールされません。 詳細については、「 [Mirror Drivers](mirror-drivers.md)」を参照してください。

 

 

 





