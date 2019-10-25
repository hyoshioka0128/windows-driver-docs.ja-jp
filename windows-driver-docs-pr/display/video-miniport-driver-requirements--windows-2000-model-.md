---
title: ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)
ms.assetid: f6ae5b71-97d5-4fd8-bd3d-7ee83f34581e
keywords:
- ビデオミニポートドライバー WDK Windows 2000、要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73bb2e37f5de95f25707bed6cd2e3ca164b6ae0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825287"
---
# <a name="video-miniport-driver-requirements-windows-2000-model"></a>ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_requirements_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_REQUIREMENTS_WINDOWS_2000_MODEL__GG"></span>


ビデオミニポートドライバーの要件の一部を次に示します。

-   **NT ベースのオペレーティングシステムのビデオミニポートドライバーは、1つの .sys ファイルである必要があり** **ます。**

    ミニポートドライバーは、1つのバイナリファイルで構成されます。 ミニポートドライバーの主な目的は、同じ種類の1つ以上のグラフィックスアダプターを検出、初期化、および構成することです。

-   **ミニポートドライバーは、 *videoprt * によってのみ呼び出しをエクスポートでき**ます **。**

    ミニポートドライバーは、システムによって提供されるビデオポートドライバーによってエクスポートされた関数のみを呼び出すことができます。 (エクスポートされたビデオポート関数は、[ビデオポートドライバーの機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に関する次の参照ページに記載されています)。また、ドライバー作成者は次のを使用して、ミニポートドライバーが呼び出している関数を特定することもできます。

    ```cpp
    link -dump -imports my_driver.sys
    ```

    ミニポートドライバーは、ドキュメント化されていないオペレーティングシステムの関数呼び出しを使用して、コンピューターに別のドライバーを読み込んだり、インストールしたりできません。

-   **ミニポートドライバーでは、エンドユーザーの要求を受け取ったときにのみ、パンを有効にできます。**

    パンは、既定で無効になっている必要があります。 ミニポートドライバーは、コントロールパネルで要求された場合にのみ有効にする必要があります。 Oem は、プレインストールの一部として、既定でパンを有効にすることができます。

 

 





