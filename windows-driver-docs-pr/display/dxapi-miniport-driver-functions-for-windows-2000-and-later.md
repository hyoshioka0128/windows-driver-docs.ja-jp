---
title: Windows 2000 以降での DxApi ミニポート ドライバーの関数
description: Windows 2000 以降での DxApi ミニポート ドライバーの関数
ms.assetid: e9a41e27-930c-49a2-b5e3-0b709b873bb3
keywords:
- DxApi ミニポート ドライバー WDK DirectDraw
- DxApi ミニポート ドライバーに関する DxApi ミニポート ドライバー WDK DirectDraw、
- autoflipping WDK DirectDraw
- フィールドの WDK DirectDraw をスキップしています
- バス WDK DirectDraw をマスター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a442ce47fac9f6414ada2387a1adcbff86efb37c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381070"
---
# <a name="dxapi-miniport-driver-functions-for-windows-2000-and-later"></a>Windows 2000 以降での DxApi ミニポート ドライバーの関数


## <span id="ddk_dxapi_miniport_driver_functions_for_windows_2000_and_later_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_FUNCTIONS_FOR_WINDOWS_2000_AND_LATER_GG"></span>


DxApi インターフェイスをサポートしている、[ビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)は Windows 2000 以降にのみサポートします。

DxApi インターフェイスのサポートは、次の操作のに役立ちます。

-   Autoflipping ハードウェア autoflipping またはをサポートしていないデバイスの IRQ を使用するには、undependable する制限があります。 これにより、DirectDraw ハードウェア autoflipping が利用できない場合、ソフトウェア autoflipping に常に戻す。

-   フィールドが IRQ を使用して MPEG データがフィルムからサンプリングされた最初の 3:2 プルダウンを元に戻すことができます MPEG ドライバーをサポートするためにスキップしています。

-   デバイスに電話しなくてもデータを継続的に転送できるように、マスターをバス[ *DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) / [*DdUnlock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)のすべてのフレーム。 これは、これらのデバイス ドライバーが WDM ドライバーのために特に便利です。

-   ビデオのキャプチャと VBI します。 ミニポート ドライバーはハードウェアのビデオ ポート IRQ またはグラフィックス IRQ に基づいてキャプチャ ビデオに簡単です。

 

 





