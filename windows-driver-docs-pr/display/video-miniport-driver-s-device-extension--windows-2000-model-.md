---
title: ビデオのミニポート ドライバーのデバイスの拡張機能 (XDDM)
description: ビデオのミニポート ドライバーのデバイス拡張機能 (Windows 2000 モデル)
ms.assetid: 4d7841d1-39e2-4bdf-b79b-3feb363a0fe5
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、デバイスの拡張機能
- デバイスの拡張機能の WDK ビデオ ミニポート
- 拡張機能の WDK ビデオのミニポート
- アダプター状態 WDK のビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 7a21b78fafd8d6f79f6c29937aaa086d453e0714
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716898"
---
# <a name="video-miniport-drivers-device-extension-windows-2000-model"></a>ビデオのミニポート ドライバーのデバイス拡張機能 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_s_device_extension_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_S_DEVICE_EXTENSION_WINDOWS_2000_MODEL__GG"></span>


デバイスの拡張機能は、アダプター固有の状態情報の各ミニポート ドライバーの唯一のグローバル プライマリ ストレージの領域です。

各ミニポート ドライバーでは、サイズ、内部構造、およびそのデバイスの拡張機能の内容を定義します。 ビデオ ポート ドライバーは、ポインターをデバイスの拡張機能を除くすべてのシステム定義のミニポート ドライバー関数への入力パラメーターとして渡します**DriverEntry** 、実装されている場合、 [ *HwVidSynchronizeExecutionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_synchronize_routine)と*SvgaHwIoPortXxx*関数。 多く**ビデオ ポート**_Xxx_関数も引数としてこのポインターを必要とします。

ミニポート ドライバーは、デバイスの拡張機能を使用して、アダプターが 1 つの状態情報を維持するためにする必要があります。 システムによって検出された各アダプターには、別のデバイスの拡張機能で管理されている別の状態情報があります。 ミニポート ドライバー、アダプターの状態を格納するのにグローバル変数を使用する必要があります。 これは、シームレスな複数を提供するために特に重要なサポートを監視します。

 

 





