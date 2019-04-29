---
title: ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)
ms.assetid: f6ae5b71-97d5-4fd8-bd3d-7ee83f34581e
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84554f990cb71f834ef8f390b844e149af581e31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389648"
---
# <a name="video-miniport-driver-requirements-windows-2000-model"></a>ビデオ ミニポート ドライバーの要件 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_requirements_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_REQUIREMENTS_WINDOWS_2000_MODEL__GG"></span>


ビデオのミニポート ドライバーの要件の一部を次に示します。

-   **オペレーティング システムの NT ベースのビデオのミニポート ドライバーは、1 つである必要があります** ***.sys*** **ファイル。**

    ミニポート ドライバーは、単一のバイナリ ファイルで構成されます。 ミニポート ドライバーの主な目的は、検出、初期化、および同じ型の 1 つまたは複数のグラフィックス アダプターを構成するのには。

-   **ミニポート ドライバーは、によってエクスポートされた呼び出しを行うことができますのみ** ***videoprt.sys* します。**

    ミニポート ドライバーでは、システム提供のビデオ ポート ドライバーによってエクスポートされる関数のみを呼び出すことができます。 (次のリファレンス ページのビデオ ポートがエクスポートされた関数が一覧表示[ビデオ ポート ドライバー機能](https://msdn.microsoft.com/library/windows/hardware/ff570533))。ドライバーの作成者は、次を使用しても、ミニポート ドライバーを呼び出す機能が決まります。

    ```cpp
    link -dump -imports my_driver.sys
    ```

    ミニポート ドライバーでは、読み込みまたはドキュメントに未記載のオペレーティング システム関数の呼び出しを使用してマシンに別のドライバーをインストールします。

-   **ミニポート ドライバーでは、エンドユーザーの要求を受信したときにのみパンを有効にできます。**

    既定では、パンを無効にする必要があります。 ミニポート ドライバーを有効にする、コントロール パネルから要求された場合にのみ。 Oem は、プレインストールの一部として既定でパンを有効にできます。

 

 





