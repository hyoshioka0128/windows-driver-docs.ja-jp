---
title: ビデオのミニポート ドライバーのデバイスの拡張機能 (XDDM)
description: ビデオのミニポート ドライバーのデバイスの拡張機能 (Windows 2000 モデル)
ms.assetid: 4d7841d1-39e2-4bdf-b79b-3feb363a0fe5
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、デバイスの拡張機能
- デバイスの拡張機能の WDK ビデオ ミニポート
- 拡張機能の WDK ビデオのミニポート
- アダプター状態 WDK のビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 017bc45c541a37a5794df40a5c2c761e5e3c4336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558389"
---
# <a name="video-miniport-drivers-device-extension-windows-2000-model"></a>ビデオのミニポート ドライバーのデバイスの拡張機能 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_s_device_extension_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_S_DEVICE_EXTENSION_WINDOWS_2000_MODEL__GG"></span>


デバイスの拡張機能は、アダプター固有の状態情報の各ミニポート ドライバーの唯一のグローバル プライマリ ストレージの領域です。

各ミニポート ドライバーでは、サイズ、内部構造、およびそのデバイスの拡張機能の内容を定義します。 ビデオ ポート ドライバーは、ポインターをデバイスの拡張機能を除くすべてのシステム定義のミニポート ドライバー関数への入力パラメーターとして渡します**DriverEntry** 、実装されている場合、 [ *HwVidSynchronizeExecutionCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff567369)と*SvgaHwIoPortXxx*関数。 多く **ビデオ ポート * * * Xxx*関数も引数としてこのポインターを必要とします。

ミニポート ドライバーは、デバイスの拡張機能を使用して、アダプターが 1 つの状態情報を維持するためにする必要があります。 システムによって検出された各アダプターには、別のデバイスの拡張機能で管理されている別の状態情報があります。 ミニポート ドライバー、アダプターの状態を格納するのにグローバル変数を使用する必要があります。 これは、シームレスな複数を提供するために特に重要なサポートを監視します。

 

 





