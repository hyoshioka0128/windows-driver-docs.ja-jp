---
title: CCD API
description: 接続して表示 (CCD) Api を構成します。
ms.assetid: b71c1582-a91c-49d8-a3a3-d20f7746c354
keywords:
- 接続が表示されます、WDK の Windows 7 の表示 CCD Api
- 接続が表示されます、WDK の Windows Server 2008 R2 の表示 CCD Api
- CCD Api WDK Windows 7 の表示を表示を構成します。
- CCD Api WDK Windows Server 2008 R2 の表示を表示を構成します。
- CCD Api WDK Windows 7 の表示
- CCD Api WDK Windows Server 2008 R2 の表示
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4561188374d6a18afd66a5b71240367f29f2458a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385679"
---
# <a name="ccd-apis"></a>CCD API


接続して表示の構成は、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみこのセクションでは (CCD) Api が適用されます。

## <a name="ccd-reference-for-user-mode-display-drivers"></a>ユーザー モードのディスプレイ ドライバーの CCD リファレンス

このセクションには接続するためのサポートを提供するリファレンス ページとユーザー モードの構成が表示されます。 ユーザー モードのディスプレイ ドライバーによっては、関数が呼び出されます。


**CCD 関数**

|||
|:--|:--|
|[DisplayConfigGetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)|[DisplayConfigSetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)|
|[GetDisplayConfigBufferSizes](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)|[QueryDisplayConfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)|
|[SetDisplayConfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)||

 
**CCD 構造体**

|||
|:--|:--|
|[DISPLAYCONFIG_2DREGION](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_2dregion)|[DISPLAYCONFIG_ADAPTER_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_adapter_name)|
|[DISPLAYCONFIG_DEVICE_INFO_HEADER](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_device_info_header)|[DISPLAYCONFIG_MODE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_mode_info)|
|[DISPLAYCONFIG_PATH_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_info)|[DISPLAYCONFIG_PATH_SOURCE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_source_info)|
|[DISPLAYCONFIG_PATH_TARGET_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_target_info)|[DISPLAYCONFIG_RATIONAL](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_rational)|
|[DISPLAYCONFIG_SET_TARGET_PERSISTENCE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_set_target_persistence)|[DISPLAYCONFIG_SOURCE_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_device_name)|
|[DISPLAYCONFIG_SOURCE_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_mode)|[DISPLAYCONFIG_TARGET_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name)|
|[DISPLAYCONFIG_TARGET_DEVICE_NAME_FLAGS](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name_flags)|[DISPLAYCONFIG_TARGET_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_mode)|
|[DISPLAYCONFIG_TARGET_PREFERRED_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_preferred_mode)|[DISPLAYCONFIG_VIDEO_SIGNAL_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)|

 
**CCD 列挙型**

|||
|:--|:--|
|[DISPLAYCONFIG_DEVICE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type)|[DISPLAYCONFIG_MODE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_mode_info_type)|
|[DISPLAYCONFIG_PIXELFORMAT](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_pixelformat)|[DISPLAYCONFIG_ROTATION](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_rotation)|
|[DISPLAYCONFIG_SCALING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scaling)|[DISPLAYCONFIG_SCANLINE_ORDERING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scanline_ordering)|
|[DISPLAYCONFIG_TOPOLOGY_ID](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_topology_id)|[DISPLAYCONFIG_VIDEO_OUTPUT_TECHNOLOGY](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)|


以下のセクションでは、CCD Api を記述し、いくつかのコード例で使用する方法を示します。

[CCD の概要とシナリオ](ccd-summaries-and-scenarios.md)

[CCD サンプル コード](ccd-example-code.md)

 

 





