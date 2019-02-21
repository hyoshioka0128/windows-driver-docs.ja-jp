---
title: CCD Ddi
description: CCD Ddi
ms.assetid: dde0e0b0-d6d0-4ca7-ae7e-427a650c080f
keywords:
- ミニポート ドライバー WDK を表示する接続と構成が表示されます (CCD)
- 接続と構成が表示されます (CCD) WDK の表示
- (接続と構成が表示されます) CCD WDK の表示
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3dd3a062c98a5413a3d0610374269e71285520b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550988"
---
# <a name="ccd-ddis"></a>CCD Ddi


Windows 7 で導入された接続と構成が表示されます (CCD) の機能は、ディスプレイ デバイスの表示が改善されましたミニポート ドライバーの制御を提供します。 

## <a name="ccd-ddis-for-display-miniport-drivers"></a>CCD Ddi 表示ミニポート ドライバー

以下の参照トピックでは、ディスプレイのミニポート ドライバーの開発に利用できる CCD デバイス ドライバー インターフェイス (Ddi) について説明します。

<span id="System-Implemented_Functions"></span><span id="system-implemented_functions"></span><span id="SYSTEM-IMPLEMENTED_FUNCTIONS"></span>**システムによって実装される関数**  

|||
|:--|:--|
|[**DXGK\_MONITOR\_INTERFACE\_V2::pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)|[**DXGK\_モニター\_インターフェイス\_V2::pfnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)|

<span id="Driver-Implemented_Function"></span><span id="driver-implemented_function"></span><span id="DRIVER-IMPLEMENTED_FUNCTION"></span>**ドライバー実装関数**

CCD をサポートする表示ミニポート ドライバーによって次の関数を実装する必要があります。

[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構造体**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_HW\_CAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)|[**D3DKMDT\_VIDPN\_PRESENT\_PATH\_SCALING\_SUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)|
|[**D3DKMT\_POLLDISPLAYCHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)|[**D3DKMT\_RENDERFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_renderflags)|
|[**DISPLAYID\_DETAILED\_タイミング\_型\_は\_縦横\_比率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|[**DXGKARG\_QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)|
|[**DXGK\_モニター\_インターフェイス\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)|[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)|
|[**DXGK\_TARGETMODE\_DETAIL\_TIMING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)||

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙型**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_PRESENT\_PATH\_SCALING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)|[**DISPLAYID\_DETAILED\_タイミング\_型\_は\_縦横\_比率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|
|[**DISPLAYID\_DETAILED\_タイミング\_型\_は\_スキャン\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_scanning_mode)|[**DISPLAYID\_DETAILED\_タイミング\_型\_は\_ステレオ\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_stereo_mode)|
|[**DISPLAYID\_DETAILED\_タイミング\_型\_は\_同期\_極性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_sync_polarity)||


表示は、ミニポート ドライバー CCD を実装する方法の詳細については、次のトピックを参照してください。

[追加のモニター ターゲット モードを取得します。](obtaining-additional-monitor-target-modes.md)

[縦横比とカスタム スケーリング モードを使用してください。](using-aspect-ratio-and-custom-scaling-modes.md)

[システム コール VidPN トポロジをお勧めします。](system-calls-to-recommend-vidpn-topology.md)

[ACPI のキーボード ショートカットのロジック](acpi-keyboard-shortcut-logic.md)

[クエリの VidPN ハードウェア機能](querying-vidpnhardware-capabilities.md)


