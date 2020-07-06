---
title: CCD API
description: ディスプレイ (CCD) Api の接続と構成
ms.assetid: b71c1582-a91c-49d8-a3a3-d20f7746c354
keywords:
- 接続により、WDK Windows 7 ディスプレイ、CCD Api が表示されます
- 接続すると、WDK Windows Server 2008 R2 ディスプレイ、CCD Api が表示されます
- '構成: WDK Windows 7 ディスプレイ、CCD Api'
- '構成: WDK Windows Server 2008 R2 ディスプレイ、CCD Api を表示します'
- CCD Api WDK Windows 7 display
- CCD Api WDK Windows Server 2008 R2 ディスプレイ
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: c001bf1f604622e38fd1292e9cee6b9c40b6d51f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968359"
---
# <a name="ccd-apis"></a>CCD API


このセクションの接続と構成のディスプレイ (CCD) Api は、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

## <a name="ccd-reference-for-user-mode-display-drivers"></a>ユーザーモード表示ドライバーの CCD リファレンス

このセクションには、ユーザーモードの表示を接続および構成するためのサポートを提供するリファレンスページが含まれています。 関数は、ユーザーモードの表示ドライバーによって呼び出されます。


**CCD 関数**

**[DisplayConfigGetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)**: [DisplayConfigSetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)

**[Getdisplayconfigbuffersizes サイズ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)**: [querydisplayconfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)

**[Setdisplayconfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)**: 


 
**CCD 構造体**

**[DISPLAYCONFIG_2DREGION](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_2dregion)**: [DISPLAYCONFIG_ADAPTER_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_adapter_name)

**[DISPLAYCONFIG_DEVICE_INFO_HEADER](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_device_info_header)**: [DISPLAYCONFIG_MODE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_mode_info)

**[DISPLAYCONFIG_PATH_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_info)**: [DISPLAYCONFIG_PATH_SOURCE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_source_info)

**[DISPLAYCONFIG_PATH_TARGET_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_target_info)**: [DISPLAYCONFIG_RATIONAL](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_rational)

**[DISPLAYCONFIG_SET_TARGET_PERSISTENCE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_set_target_persistence)**: [DISPLAYCONFIG_SOURCE_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_device_name)

**[DISPLAYCONFIG_SOURCE_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_mode)**: [DISPLAYCONFIG_TARGET_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name)

**[DISPLAYCONFIG_TARGET_DEVICE_NAME_FLAGS](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name_flags)**: [DISPLAYCONFIG_TARGET_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_mode)

**[DISPLAYCONFIG_TARGET_PREFERRED_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_preferred_mode)**: [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)


 
**CCD 列挙型**

**[DISPLAYCONFIG_DEVICE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type)**: [DISPLAYCONFIG_MODE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_mode_info_type)

**[DISPLAYCONFIG_PIXELFORMAT](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_pixelformat)**: [DISPLAYCONFIG_ROTATION](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_rotation)

**[DISPLAYCONFIG_SCALING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scaling)**: [DISPLAYCONFIG_SCANLINE_ORDERING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scanline_ordering)

**[DISPLAYCONFIG_TOPOLOGY_ID](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_topology_id)**: [DISPLAYCONFIG_VIDEO_OUTPUT_TECHNOLOGY](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)



次のセクションでは、CCD Api について説明し、いくつかのコード例でそれらを使用する方法を示します。

[CCD の概要とシナリオ](ccd-summaries-and-scenarios.md)

[CCD コード例](ccd-example-code.md)

 

 





