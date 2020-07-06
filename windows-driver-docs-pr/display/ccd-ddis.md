---
title: CCD DDI
description: CCD DDI
ms.assetid: dde0e0b0-d6d0-4ca7-ae7e-427a650c080f
keywords:
- ミニポートドライバー WDK ディスプレイ、接続、構成ディスプレイ (CCD)
- ディスプレイ (CCD) WDK ディスプレイの接続と構成
- CCD (接続と構成の表示) WDK ディスプレイ
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c6581da4e607e3be4fe399edfa6fa4149cd0a82
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968489"
---
# <a name="ccd-ddis"></a>CCD DDI


Windows 7 で導入された接続と構成の表示 (CCD) 機能により、ディスプレイデバイスのディスプレイミニポートドライバーの制御が向上しました。 

## <a name="ccd-ddis-for-display-miniport-drivers"></a>ミニポートドライバーを表示するための CCD DDIs

次の参照トピックでは、ミニポートドライバーを表示する開発者が使用できる CCD デバイスドライバーインターフェイス (DDIs) について説明します。

<span id="System-Implemented_Functions"></span><span id="system-implemented_functions"></span><span id="SYSTEM-IMPLEMENTED_FUNCTIONS"></span>**システム実装関数**  

**[**DXGK \_Monitor \_ interface \_ v2::p fngetadditionalmonitormodeset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)**: [ **DXGK \_ monitor \_ interface \_ v2::p fnreleaseadditionalmonitormodeset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)


<span id="Driver-Implemented_Function"></span><span id="driver-implemented_function"></span><span id="DRIVER-IMPLEMENTED_FUNCTION"></span>**ドライバーによって実装された関数**

次の関数は、CCD をサポートする表示ミニポートドライバーによって実装される必要があります。

[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構成**

**[**D3DKMDT \_Vidpn \_ HW \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)**: [ **D3DKMDT \_ VIDPN の \_ 現在の \_ パス \_ スケーリング \_ サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)

**[**D3DKMT \_Polldisplaychildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)**: [ **D3DKMT \_ renderflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_renderflags)

**[**Displayid \_詳細な \_ タイミングの \_ 種類 \_ I \_ 縦横 \_ 比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)**: [ **DXGKARG \_ QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)

**[**DXGK \_MONITOR \_ INTERFACE \_ V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)**: [ **DXGK の \_ プレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)

**[**DXGK \_TARGETMODE の \_ 詳細な \_ タイミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)**: 


<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙**

**[**D3DKMDT \_VIDPN \_ PRESENT \_ パスの \_ スケーリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)**: [ **DISPLAYID \_ 詳細な \_ タイミングの \_ 種類 \_ I \_ 縦横 \_ 比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)

**[**Displayid \_詳細な \_ タイミングの \_ 種類の \_ \_ スキャン \_ モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_scanning_mode)**: [ **DISPLAYID \_ 詳細な \_ タイミングの \_ 種類 \_ I \_ ステレオ \_ モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_stereo_mode)

**[**Displayid \_詳細な \_ タイミングの \_ 種類 \_ \_ 同期 \_ 極性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_sync_polarity)**: 



ディスプレイミニポートドライバーに CCD を実装する方法の詳細については、次のトピックを参照してください。

[追加のモニター ターゲット モードの取得](obtaining-additional-monitor-target-modes.md)

[縦横比とカスタム スケーリング モードの使用](using-aspect-ratio-and-custom-scaling-modes.md)

[推奨される VidPN トポロジへのシステム コール](system-calls-to-recommend-vidpn-topology.md)

[ACPI キーボード ショートカット ロジック](acpi-keyboard-shortcut-logic.md)

[VidPN ハードウェア機能のクエリ](querying-vidpnhardware-capabilities.md)


