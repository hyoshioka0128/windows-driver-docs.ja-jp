---
title: ビデオミニポートドライバーのデバイス拡張機能 (XDDM)
description: ビデオのミニポート ドライバーのデバイス拡張機能 (Windows 2000 モデル)
ms.assetid: 4d7841d1-39e2-4bdf-b79b-3feb363a0fe5
keywords:
- ビデオミニポートドライバー WDK Windows 2000、デバイス拡張機能
- デバイス拡張機能 WDK ビデオミニポート
- 拡張機能の WDK ビデオミニポート
- アダプターの状態 WDK ビデオミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: dfa5bb113cc24451d2e115825fe3cbf8a0100e44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829191"
---
# <a name="video-miniport-drivers-device-extension-windows-2000-model"></a>ビデオのミニポート ドライバーのデバイス拡張機能 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_s_device_extension_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_S_DEVICE_EXTENSION_WINDOWS_2000_MODEL__GG"></span>


デバイス拡張機能は、各ミニポートドライバーのプライマリと、アダプター固有の状態情報のグローバルストレージ領域のみです。

各ミニポートドライバーは、デバイス拡張機能のサイズ、内部構造、および内容を定義します。 ビデオポートドライバーは、 **Driverentry**を除くすべてのシステム定義のミニポートドライバー関数への入力パラメーターとしてデバイス拡張機能へのポインターを渡します。また、実装されている場合は、 [*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)と*Svガス hwioportxxx を返します。* 関数。 多くの**VideoPort**_Xxx_関数では、このポインターが引数としても必要です。

また、ミニポートドライバーは、デバイス拡張機能を使用して、1つのアダプターの状態情報を維持する必要があります。 システムによって検出された各アダプターには、個別のデバイス拡張機能で保持される個別の状態情報が含まれます。 ミニポートドライバーは、アダプターごとの状態を格納するためにグローバル変数を使用することはできません。 これは、複数のモニターをシームレスにサポートするために特に重要です。

 

 





